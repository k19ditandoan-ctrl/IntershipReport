---
title: "AWS Cloud Deployment"
date: 2026-04-03
weight: 12
chapter: false
pre: " <b> 5.12. </b> "
---

#### Production Deployment Overview

After developing and testing on the local environment, the next step is deploying Slothub to **AWS Cloud** for production. The architecture follows a **serverless container** model using **Amazon ECS on Fargate**, ensuring auto-scaling capabilities and minimizing infrastructure management overhead.

#### Production Architecture on AWS

```
                         ┌─────────────┐
                         │  Route 53   │ ← DNS domain
                         └──────┬──────┘
                                │
                         ┌──────▼──────┐
                         │   AWS WAF   │ ← Web protection
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

#### 1. Containerization with Docker & ECR

Each microservice is packaged as a Docker image and pushed to **Amazon ECR (Elastic Container Registry)**:

##### Backend Dockerfile (Spring Boot)

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

##### AI Service Dockerfile (FastAPI)

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

##### Pushing Images to ECR

```bash
# Login to ECR
aws ecr get-login-password --region ap-southeast-1 | \
  docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com

# Build & tag
docker build -t slothub-backend ./backend
docker tag slothub-backend:latest <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/slothub-backend:latest

# Push
docker push <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/slothub-backend:latest
```

#### 2. Amazon ECS on Fargate

Fargate enables running containers **without managing servers** (serverless containers). Task Definition configuration for each service:

| Service | CPU | Memory | Port |
|---------|-----|--------|------|
| Backend (Spring Boot) | 512 vCPU | 1024 MB | 8080 |
| AI Service (FastAPI) | 256 vCPU | 512 MB | 8000 |
| Agent-Core (Slozy) | 256 vCPU | 512 MB | — |

{{% notice tip %}}
Use **right-sizing** to optimize costs: start with a low configuration, monitor via CloudWatch, and scale up as needed. Fargate allows flexible CPU/Memory adjustments.
{{% /notice %}}

#### 3. Application Load Balancer (ALB)

The ALB distributes traffic to Fargate tasks through target groups:

```
ALB Rules:
  /api/*          → Target Group: Backend (Fargate, port 8080)
  /api/v1/*       → Target Group: AI Service (Fargate, port 8000)
  /*              → Target Group: Frontend (Amplify redirect)
```

#### 4. Amazon RDS PostgreSQL (Multi-AZ)

The production database uses **Amazon RDS** instead of Docker Compose:

| Configuration | Value |
|--------------|-------|
| Engine | PostgreSQL 15 |
| Instance | db.t3.micro (dev) / db.t3.medium (prod) |
| Storage | 20 GB (auto-scaling) |
| Multi-AZ | Enabled (Primary + Standby) |
| Backup | Automated, 7-day retention |
| Extension | pgvector (for RAG) |

```bash
# Enable pgvector extension on RDS
psql -h your-rds-endpoint -d EDU_CARE -U postgres
CREATE EXTENSION IF NOT EXISTS vector;
```

{{% notice warning %}}
Ensure your RDS PostgreSQL instance is placed in a **Private Subnet** — only allow access from Fargate tasks via Security Groups, never expose to the public internet.
{{% /notice %}}

#### 5. AWS Amplify (Frontend Hosting)

The React frontend is deployed via **AWS Amplify** with automatic CI/CD:

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

#### 6. CI/CD with GitHub Actions

An automated pipeline builds, tests, and deploys on code push:

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

#### 7. Security & Monitoring

##### AWS WAF (Web Application Firewall)
- Blocks SQL injection, XSS, request flooding
- Rate limiting for API endpoints

##### Amazon Cognito
- Centralized user management
- Social Login support (Google, Facebook)
- MFA (Multi-Factor Authentication)

##### AWS Certificate Manager (ACM)
- Free SSL/TLS certificates for HTTPS
- Automatic renewal

##### Amazon CloudWatch
```
Monitoring metrics:
├── ECS/Fargate: CPU, Memory, Task count
├── ALB: Request count, Latency, Error rate
├── RDS: Connections, Read/Write IOPS, Free storage
└── Custom: API response time, AI generation time
```

##### Amazon GuardDuty
- Automated threat detection
- Anomalous access alerting
- IAM credentials monitoring

#### AWS Services Summary

| Service | Role |
|---------|------|
| **Route 53** | DNS, domain routing |
| **WAF** | Web application protection |
| **Amplify** | React frontend hosting |
| **ACM** | SSL/TLS certificates |
| **ALB** | Load balancing |
| **ECS/Fargate** | Backend & AI container runtime |
| **ECR** | Docker image registry |
| **RDS PostgreSQL** | Production database (Multi-AZ) |
| **S3** | Document storage |
| **Bedrock AgentCore** | Slozy AI agent |
| **Cognito** | User authentication |
| **CloudWatch** | Monitoring & logging |
| **GuardDuty** | Threat detection |

{{% notice info %}}
The entire AWS architecture is designed for deployment in the **ap-southeast-1 (Singapore)** region, optimizing latency for Vietnamese users. Use **Multi-AZ** for RDS and distribute Fargate tasks across multiple Availability Zones to ensure high availability.
{{% /notice %}}

Congratulations on completing the detailed Slothub workshop! Return to the **Cleanup** section if you need to release resources after practicing.
