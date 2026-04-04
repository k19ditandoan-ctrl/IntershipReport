---
title: "Triển khai AWS Cloud"
date: 2026-04-03
weight: 12
chapter: false
pre: " <b> 5.12. </b> "
---

#### Tổng quan Triển khai Production

Sau khi phát triển và kiểm thử trên môi trường local, bước tiếp theo là đưa Slothub lên **AWS Cloud** để triển khai production. Kiến trúc được thiết kế theo mô hình **serverless container** sử dụng **Amazon ECS on Fargate**, đảm bảo khả năng mở rộng (auto-scaling) và giảm thiểu chi phí vận hành hạ tầng.

#### Kiến trúc Production trên AWS

```
                         ┌─────────────┐
                         │  Route 53   │ ← DNS tên miền
                         └──────┬──────┘
                                │
                         ┌──────▼──────┐
                         │   AWS WAF   │ ← Bảo vệ web
                         └──────┬──────┘
                                │
              ┌─────────────────┼─────────────────┐
              │                                   │
       ┌──────▼──────┐                     ┌──────▼──────┐
       │  Amplify     │                     │    ALB      │
       │ (Frontend)   │                     │ (Load Bal.) │
       └─────────────┘                     └──────┬──────┘
                                                  │
                                    ┌─────────────┼──────────────┐
                                    │                            │
                             ┌──────▼──────┐              ┌─────▼──────┐
                             │  Fargate    │              │  Fargate   │
                             │ (Backend)   │              │ (AI Svc)   │
                             └──────┬──────┘              └─────┬──────┘
                                    │                            │
                                    └──────────┬─────────────────┘
                                               │
                                    ┌──────────▼──────────┐
                                    │  RDS PostgreSQL     │
                                    │  (Multi-AZ)         │
                                    └─────────────────────┘
```

#### 1. Container hóa với Docker & ECR

Mỗi microservice được đóng gói thành Docker image và đẩy lên **Amazon ECR (Elastic Container Registry)**:

##### Dockerfile cho Backend (Spring Boot)

```dockerfile
FROM eclipse-temurin:17-jdk-alpine AS builder
WORKDIR /app
COPY pom.xml mvnw ./
COPY .mvn .mvn
RUN ./mvnw dependency:resolve
COPY src src
RUN ./mvnw package -DskipTests

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

##### Dockerfile cho AI Service (FastAPI)

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

##### Push Image lên ECR

```bash
# Đăng nhập ECR
aws ecr get-login-password --region ap-southeast-1 | \
  docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com

# Build & tag
docker build -t slothub-backend ./backend
docker tag slothub-backend:latest <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/slothub-backend:latest

# Push
docker push <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/slothub-backend:latest
```

#### 2. Amazon ECS on Fargate

Fargate cho phép chạy container **không cần quản lý server** (serverless container). Cấu hình Task Definition cho mỗi service:

| Service | CPU | Memory | Port |
|---------|-----|--------|------|
| Backend (Spring Boot) | 512 vCPU | 1024 MB | 8080 |
| AI Service (FastAPI) | 256 vCPU | 512 MB | 8000 |
| Agent-Core (Slozy) | 256 vCPU | 512 MB | — |

{{% notice tip %}}
Sử dụng **right-sizing** để tối ưu chi phí: bắt đầu với cấu hình thấp, giám sát qua CloudWatch, tăng dần khi cần thiết. Fargate cho phép điều chỉnh CPU/Memory linh hoạt.
{{% /notice %}}

#### 3. Application Load Balancer (ALB)

ALB phân phối traffic đến các Fargate tasks qua target groups:

```
ALB Rules:
  /api/*          → Target Group: Backend (Fargate, port 8080)
  /api/v1/*       → Target Group: AI Service (Fargate, port 8000)
  /*              → Target Group: Frontend (Amplify redirect)
```

#### 4. Amazon RDS PostgreSQL (Multi-AZ)

Database production sử dụng **Amazon RDS** thay vì Docker Compose:

| Cấu hình | Giá trị |
|-----------|---------|
| Engine | PostgreSQL 15 |
| Instance | db.t3.micro (dev) / db.t3.medium (prod) |
| Storage | 20 GB (auto-scaling) |
| Multi-AZ | Enabled (Primary + Standby) |
| Backup | Tự động, retention 7 ngày |
| Extension | pgvector (cho RAG) |

```bash
# Kích hoạt pgvector extension trên RDS
psql -h your-rds-endpoint -d EDU_CARE -U postgres
CREATE EXTENSION IF NOT EXISTS vector;
```

{{% notice warning %}}
Đảm bảo RDS PostgreSQL được đặt trong **Private Subnet** — chỉ cho phép truy cập từ Fargate tasks thông qua Security Group, không mở public internet.
{{% /notice %}}

#### 5. AWS Amplify (Frontend Hosting)

Frontend React được deploy qua **AWS Amplify** với CI/CD tự động:

```yaml
# amplify.yml - Build configuration
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - npm install
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

#### 6. CI/CD với GitHub Actions

Pipeline tự động build, test và deploy khi push code:

```yaml
# .github/workflows/deploy.yml
name: Deploy to AWS
on:
  push:
    branches: [main]

jobs:
  deploy-backend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-southeast-1
      
      - name: Login to ECR
        uses: aws-actions/amazon-ecr-login@v2
      
      - name: Build & Push Docker image
        run: |
          docker build -t slothub-backend ./backend
          docker tag slothub-backend:latest $ECR_REGISTRY/slothub-backend:latest
          docker push $ECR_REGISTRY/slothub-backend:latest
      
      - name: Update ECS Service
        run: |
          aws ecs update-service \
            --cluster slothub-cluster \
            --service slothub-backend \
            --force-new-deployment
```

#### 7. Bảo mật & Giám sát

##### AWS WAF (Web Application Firewall)
- Chặn SQL injection, XSS, request flood
- Rate limiting cho API endpoints

##### Amazon Cognito
- Quản lý người dùng tập trung
- Hỗ trợ Social Login (Google, Facebook)
- MFA (Multi-Factor Authentication)

##### AWS Certificate Manager (ACM)
- SSL/TLS certificate miễn phí cho HTTPS
- Tự động renew

##### Amazon CloudWatch
```
Metrics giám sát:
├── ECS/Fargate: CPU, Memory, Task count
├── ALB: Request count, Latency, Error rate
├── RDS: Connections, Read/Write IOPS, Free storage
└── Custom: API response time, AI generation time
```

##### Amazon GuardDuty
- Phát hiện mối đe dọa bảo mật tự động
- Cảnh báo truy cập bất thường
- Giám sát IAM credentials

#### Tổng kết Dịch vụ AWS

| Dịch vụ | Vai trò |
|---------|---------|
| **Route 53** | DNS, định tuyến tên miền |
| **WAF** | Bảo vệ web application |
| **Amplify** | Hosting frontend React |
| **ACM** | Chứng chỉ SSL/TLS |
| **ALB** | Cân bằng tải |
| **ECS/Fargate** | Chạy backend & AI containers |
| **ECR** | Registry Docker images |
| **RDS PostgreSQL** | Database production (Multi-AZ) |
| **S3** | Lưu trữ tài liệu |
| **Bedrock AgentCore** | Agent AI Slozy |
| **Cognito** | Xác thực người dùng |
| **CloudWatch** | Giám sát & logging |
| **GuardDuty** | Phát hiện mối đe dọa |

{{% notice info %}}
Toàn bộ kiến trúc AWS được thiết kế để triển khai tại region **ap-southeast-1 (Singapore)**, tối ưu latency cho người dùng Việt Nam. Sử dụng **Multi-AZ** cho RDS và phân tán Fargate tasks trên nhiều Availability Zone để đảm bảo tính sẵn sàng cao.
{{% /notice %}}

Chúc mừng bạn đã hoàn thành workshop chi tiết về Slothub! Quay lại phần **Dọn dẹp** nếu bạn cần giải phóng tài nguyên sau khi thực hành.
