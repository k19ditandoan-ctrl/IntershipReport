---
title: "Phát triển & Triển khai"
date: 2026-04-03
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Chạy Các Microservices Ở Local

Slothub yêu cầu liên kết 4 quá trình phân tán để hoạt động. Trong thực tế, toàn bộ quá trình này sẽ được đóng gói chạy trên các container clusters ví dụ như AWS ECS (Fargate). Ở workshop này, chúng ta sẽ bắt đầu khởi động tuần tự qua local bằng các tệp `.env`. Hãy đảm bảo bạn có thông số `.env` đúng dựa theo `report.md`.

##### 1. Khởi động Backend API (Spring Boot)
Backend kết nối tới PosgreSQL và thiết lập logic.

* Khởi động terminal tại thư mục `backend/`.
* Bổ sung đầy đủ cho `DB_HOST`, `JWT_SIGNER_KEY`, email, và AWS keys vào file.
* Tiến hành chạy hệ thống:
  ```bash
  ./mvnw spring-boot:run
  ```
Spring Boot sẽ sẵn sàng xử lý request qua cổng `8080`.

##### 2. Khởi động Dịch Vụ AI Content (FastAPI)
Bên trung gian quản lý tiến trình của OpenAI và AWS S3.

* Khởi động terminal ở thư mục `AI/`.
* Xác thực `OPENAI_API_KEY` cũng như môi trường S3.
* Kích hoạt môi trường và giao thức Uvicorn API:
  ```bash
  uvicorn main:app --host 0.0.0.0 --port 8000
  ```
Dịch vụ content tự sinh này phục vụ trên luồng `http://localhost:8000/api/v1`.

##### 3. Khởi động LangGraph Agent-Core (Slozy)
Máy học tương tác truy xuất RAG trên Pgvector.

* Dùng Terminal với thư mục `agent-core/`.
* Gán giá trị `LOCAL_DEV=1` ở file `.env` nếu bạn không muốn chi trả cho AWS Bedrock trên Test Env.
* Khởi động script. (Hãy đảm bảo bạn hoàn tất lệnh `pip install -r requirements.txt`).

##### 4. Khởi động Giao Diện (React Vite)
Thành phần đồng nhất cho Users.

* Chuyển đến thư mục `frontend/`.
* Chắc chắn `VITE_API_BASE_URL` nối tới cổng `8080` (Spring Boot) và `VITE_FAST_API_BASE_URL` nối tới cổng `8000` theo file `.env`.
* Build thư viện và Test:
  ```bash
  npm install
  npm run dev
  ```

Trải nghiệm hệ thống ở `http://localhost:5173`. Tham gia đăng nhập lớp học, upload PDF lấy bài tập, và bắt đầu hội thoại với Gia sư AI xem các widgets render từ React như thế nào để chứng minh rằng 4 máy chủ đã liên kết thành công!
