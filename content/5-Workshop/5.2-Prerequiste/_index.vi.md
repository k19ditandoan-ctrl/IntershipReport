---
title: "Yêu cầu tiên quyết"
date: 2026-04-03
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Các yêu cầu tiên quyết

Để thiết lập kiến trúc microservice của Slothub trên môi trường nội bộ (local), bạn sẽ cần chuẩn bị các công cụ và tài khoản sau:

#### 1. Môi trường phát triển
- **Java Development Kit (JDK) 17**: Yêu cầu bắt buộc để build và chạy dịch vụ Spring Boot backend.
- **Node.js (v18 trở lên) & npm**: Cần thiết để khởi chạy frontend React/TypeScript/Vite.
- **Python (3.10 đến 3.12)**: Sử dụng cho FastAPI AI Service (khuyến nghị bản 3.12) và LangGraph Agent-Core (khuyến nghị bản 3.10).
- **Docker & Docker Compose**: Cách dễ nhất để khởi chạy cơ sở dữ liệu PostgreSQL dùng chung kèm theo extension `pgvector` phục vụ vector search.
- **Git**: Dùng để clone và quản lý mã nguồn.

#### 2. Tài khoản Cloud & Cấp khóa API
Do dự án tích hợp hệ thống AI đa tầng, bạn sẽ cần chuẩn bị thông tin xác thực cho các dịch vụ đám mây sau:
- **Tài khoản AWS**:
  - Sở hữu một **S3 Bucket** (ví dụ: ở region `ap-southeast-1`) để lưu trữ file tài liệu PDF hoặc bài tập sinh ra.
  - Cấp quyền Access key (`AWS_ACCESS_KEY`, `AWS_SECRET_KEY`) có khả năng đẩy/đọc file từ S3 và gọi dịch vụ AWS Bedrock.
- **OpenAI API Key**: Được sử dụng bởi dịch vụ FastAPI để nhúng (embeddings) và thực thi các tác vụ sinh nội dung giáo dục.

#### 3. IDE / Trình chỉnh sửa code
- **Visual Studio Code** hoặc **IntelliJ IDEA**: Dùng cho phát triển frontend và backend.
- **pgAdmin** hoặc **DBeaver**: Để thao tác với dữ liệu, có thể truy cập qua pgAdmin được cài đặt chung trong file `docker-compose.yml`.

Sau khi cài đặt đầy đủ các phần mềm và chuẩn bị xong API keys, bạn đã sẵn sàng đi tiếp tới phần cấu trúc dự án và chạy các đoạn mã đầu tiên.
