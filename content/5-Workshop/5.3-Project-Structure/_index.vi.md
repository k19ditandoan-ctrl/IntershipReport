---
title: "Cấu trúc dự án"
date: 2026-04-03
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Cấu trúc thư mục của Slothub

Dự án được cấu trúc dưới dạng một mono-repository bao gồm 4 dịch vụ cực kỳ độc lập (microservices). Mỗi dịch vụ có thể được phát triển và scale một cách riêng biệt. Dưới đây là tổng quan về các thư mục:

```text
Slothub/
├── frontend/
│   ├── src/                 # Chứa mã nguồn React (components, pages)
│   ├── public/              # Chứa các tài sản tĩnh (ảnh, icon)
│   ├── package.json         # Danh sách thư viện Node.js
│   └── .env                 # Điểm cuối API Base URLs
├── backend/
│   ├── src/main/java        # Mã nguồn Java Spring Boot
│   ├── src/main/resources   # File cấu hình ứng dụng application.yml
│   ├── pom.xml              # Cấu hình cài đặt Maven
│   └── .env                 # Thông tin đăng nhập Database & JWT
├── AI/
│   ├── main.py              # Điểm khởi chạy của FastAPI
│   ├── services/            # Tích hợp OpenAI và kỹ năng xử lý S3
│   ├── requirements.txt     # Thư viện Python
│   └── .env                 # OpenAI API key, cấu hình S3 Bucket
├── agent-core/
│   ├── app.py               # Định nghĩa LangGraph và logic cho Agent
│   ├── tools/               # Các công cụ của Bedrock (RAG, lộ trình, câu hỏi)
│   ├── requirements.txt     # Thư viện Python dành riêng cho Agent
│   └── .env                 # AWS credentials để test ở Local
└── docker-compose.yml       # Chứa Postgres Database và pgAdmin dùng chung
```

#### Hiểu về các thành phần

- `frontend/`: Giao diện người dùng được xây dựng bằng React. Khác biệt lớn nhất là nó có khả năng linh hoạt hiển thị các khối nội dung (widgets) được gửi trả về từ agent thông qua giao thức (`>>>[UI_WIDGET:TYPE|args]<<<`).
- `backend/`: Trái tim điều phối hệ thống cơ bản. Nó cung cấp API quản lý Người dùng và Lớp học, cấp phát JWT qua kiến trúc OAuth2 resource server.
- `AI/`: Nhà máy sản xuất nội dung số. Khi giáo viên tải lên tài liệu PDF, dịch vụ này sẽ dùng nội dung từ OpenAI để sinh ra bài tập và câu hỏi ôn tập một cách tự động, kèm theo đó là lưu trữ mọi file kết quả lên bucket tại AWS S3.
- `agent-core/`: Bộ não tư duy (Gia sư AI Slozy). Được vận hành với LangGraph framework, thành phần này xử lý hỏi đáp theo thời gian thực từ học sinh. Thông qua việc quét thông tin trên module `pgvector` từ Postgres, bộ não này đáp ứng chính xác về mặt lý thuyết với phương pháp RAG.

Ở phần sau, chúng ta sẽ bắt đầu khởi tạo lớp cơ sở hạ tầng (Database & AWS) qua cấu hình Docker Compose.
