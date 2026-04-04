---
title: "Cấu hình Biến Môi trường"
date: 2026-04-03
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Tổng quan về Biến Môi trường

Kiến trúc microservice của Slothub yêu cầu mỗi dịch vụ phải được cấu hình thông qua các file `.env` riêng biệt. Việc quản lý biến môi trường đúng cách là yếu tố then chốt để các dịch vụ giao tiếp trơn tru với nhau và với các dịch vụ đám mây bên ngoài.

{{% notice warning %}}
**Không bao giờ** commit file `.env` lên Git repository. Hãy đảm bảo `.env` đã được liệt kê trong `.gitignore` để bảo vệ thông tin nhạy cảm như API keys và database credentials.
{{% /notice %}}

#### 1. Frontend (`frontend/.env`)

Frontend React cần biết địa chỉ của 2 API Backend để gửi request:

```env
# Địa chỉ API Spring Boot Backend
VITE_API_BASE_URL=http://localhost:8080/api

# Địa chỉ API FastAPI (AI Service)
VITE_FAST_API_BASE_URL=http://localhost:8000/api/v1
```

| Biến | Mô tả | Giá trị mặc định |
|------|--------|-------------------|
| `VITE_API_BASE_URL` | Endpoint REST API chính (Spring Boot) | `http://localhost:8080/api` |
| `VITE_FAST_API_BASE_URL` | Endpoint AI Service (FastAPI) | `http://localhost:8000/api/v1` |

{{% notice tip %}}
Prefix `VITE_` là bắt buộc để Vite inject biến vào bundle JavaScript phía client. Các biến không có prefix này sẽ không khả dụng trong mã nguồn React.
{{% /notice %}}

#### 2. Backend (`backend/.env`)

Backend Spring Boot cần kết nối đến PostgreSQL, cấu hình JWT và email:

```env
# Kết nối Database
DB_HOST=localhost
DB_NAME=EDU_CARE
DB_USERNAME=postgres
DB_PASSWORD=your_password

# JWT Authentication
JWT_SIGNER_KEY=your_256bit_secret_key_here

# AWS Credentials (cho upload file)
AWS_ACCESS_KEY=AKIAxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Gmail SMTP (cho chức năng reset mật khẩu)
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_app_password
```

| Biến | Mô tả | Ghi chú |
|------|--------|---------|
| `DB_HOST` | Địa chỉ PostgreSQL | `localhost` khi dùng Docker Compose |
| `DB_NAME` | Tên database | Mặc định là `EDU_CARE` |
| `DB_USERNAME` | Tài khoản DB | Thường là `postgres` |
| `DB_PASSWORD` | Mật khẩu DB | Được thiết lập trong `docker-compose.yml` |
| `JWT_SIGNER_KEY` | Khóa bí mật để ký JWT tokens | Nên dùng chuỗi ngẫu nhiên 256-bit |
| `AWS_ACCESS_KEY` | AWS IAM Access Key | Cần quyền S3 |
| `AWS_SECRET_KEY` | AWS IAM Secret Key | Bảo mật tuyệt đối |
| `MAIL_USERNAME` | Tài khoản Gmail SMTP | Dùng cho gửi email reset password |
| `MAIL_PASSWORD` | App Password của Gmail | Tạo từ Google Account → App Passwords |

#### 3. AI Service (`AI/.env`)

Dịch vụ FastAPI cần kết nối DB trực tiếp, OpenAI API và AWS S3:

```env
# Database (kết nối trực tiếp qua psycopg2)
DB_HOST=localhost
DB_NAME=EDU_CARE
DB_USERNAME=postgres
DB_PASSWORD=your_password

# AWS S3 Configuration
AWS_ACCESS_KEY=AKIAxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_REGION=ap-southeast-1
AWS_BUCKET_NAME=Slothub-upload-2026

# OpenAI API
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

{{% notice info %}}
Dịch vụ AI kết nối **trực tiếp** tới PostgreSQL thông qua thư viện `psycopg2`, không qua ORM. Service này tự động chạy migration (tạo bảng nếu chưa có) mỗi khi khởi động.
{{% /notice %}}

#### 4. Agent-Core (`agent-core/.env`)

Agent-Core (Slozy AI Tutor) cần AWS credentials và flag dev mode:

```env
# Database
DB_HOST=localhost
DB_NAME=EDU_CARE
DB_USERNAME=postgres
DB_PASSWORD=your_password

# AWS Credentials
AWS_ACCESS_KEY=AKIAxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_REGION=ap-southeast-1
AWS_BUCKET_NAME=Slothub-upload-2026

# OpenAI (dùng chung embedding model)
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Chế độ phát triển Local
LOCAL_DEV=1
```

| Biến | Mô tả | Giá trị |
|------|--------|---------|
| `LOCAL_DEV` | Khi bằng `1`, agent sử dụng `MemorySaver` (RAM) thay vì `AgentCoreMemorySaver` (AWS Bedrock) | `1` cho local, bỏ hoặc `0` cho production |

{{% notice warning %}}
Khi `LOCAL_DEV=1`, lịch sử hội thoại sẽ **mất** khi restart agent. Trên production, hãy tắt flag này để dùng `AgentCoreMemorySaver` lưu trữ bền vững qua AWS Bedrock.
{{% /notice %}}

#### Kiểm tra toàn bộ cấu hình

Sau khi hoàn tất thiết lập `.env` cho cả 4 dịch vụ, hãy xác nhận bằng checklist:

- [ ] `frontend/.env` — 2 URL endpoints đã chỉ đúng port
- [ ] `backend/.env` — Kết nối DB thành công, JWT key đã set
- [ ] `AI/.env` — OpenAI key hợp lệ, S3 bucket tồn tại
- [ ] `agent-core/.env` — `LOCAL_DEV=1` để test, AWS credentials sẵn sàng

Tiếp theo, chúng ta sẽ đi sâu vào kiến trúc Backend Spring Boot và các domain chính của hệ thống.
