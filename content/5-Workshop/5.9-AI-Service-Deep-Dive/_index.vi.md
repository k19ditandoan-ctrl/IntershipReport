---
title: "Dịch vụ AI (FastAPI)"
date: 2026-04-03
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

#### Tổng quan Dịch vụ AI

Dịch vụ AI của Slothub được xây dựng bằng **Python 3.12 + FastAPI**, hoạt động như một nhà máy sản xuất nội dung giáo dục tự động. Dịch vụ chạy trên cổng `8000` và xử lý ba nhiệm vụ chính: **sinh bài tập**, **tạo lộ trình học**, và **quản lý tài liệu**.

#### Kiến trúc Dịch vụ

```text
AI/
├── main.py                # Điểm khởi chạy FastAPI - định nghĩa routes
├── services/
│   ├── openai_service.py  # Tích hợp OpenAI (embedding + generation)
│   ├── s3_service.py      # Upload/download file từ AWS S3
│   ├── document_service.py# Xử lý tài liệu PDF
│   └── roadmap_service.py # Logic sinh lộ trình học
├── models/                # Pydantic models cho request/response
├── requirements.txt       # Dependencies Python
└── .env                   # Cấu hình môi trường
```

#### Tính năng chính

##### 1. Sinh Bài tập Tự động từ PDF

Khi giáo viên tải lên tài liệu PDF, quy trình xử lý diễn ra như sau:

```
1. Giáo viên upload PDF qua Frontend
2. Frontend gửi file đến FastAPI endpoint
3. FastAPI lưu file lên AWS S3 (bucket: Slothub-upload-2026)
4. Trích xuất nội dung text từ PDF
5. Gửi nội dung tới OpenAI API để phân tích
6. OpenAI sinh ra bài tập/câu hỏi dựa trên nội dung
7. Kết quả trả về cho Frontend hiển thị
```

{{% notice tip %}}
File được lưu trữ có cấu trúc trên S3 với region `ap-southeast-1`, sử dụng naming convention theo classroom và subject để dễ quản lý.
{{% /notice %}}

##### 2. Tạo Lộ trình Học (Roadmap)

Endpoint `/roadmap` phân tích kiến thức hiện tại của học sinh và tạo lộ trình ôn tập cá nhân hóa:

```python
# Ví dụ flow tạo roadmap
POST /api/v1/roadmap
{
    "subject": "Toán 12",
    "current_level": "trung bình",
    "target": "kỳ thi cuối kỳ",
    "weeks_available": 4
}

# Response: Lộ trình chi tiết theo tuần
{
    "roadmap": [
        {"week": 1, "topics": ["Đạo hàm", "Cực trị"], "exercises": 15},
        {"week": 2, "topics": ["Tích phân cơ bản"], "exercises": 20},
        ...
    ]
}
```

##### 3. Proxy Chat tới Agent Slozy

FastAPI đóng vai trò **proxy trung gian** cho tin nhắn chat, chuyển tiếp từ frontend tới Agent-Core (Slozy AI):

```
Frontend → FastAPI (proxy) → Agent-Core (Slozy)
                                ↓
                          AWS Bedrock AgentCore
                                ↓
                       PostgreSQL pgvector (RAG)
```

#### Tích hợp OpenAI API

Dịch vụ sử dụng **OpenAI API** cho hai mục đích:

| Chức năng | Model | Mô tả |
|-----------|-------|--------|
| **Embedding** | `text-embedding-ada-002` | Chuyển đổi text thành vector để lưu vào pgvector |
| **Generation** | `gpt-4` / `gpt-3.5-turbo` | Sinh nội dung giáo dục (bài tập, lộ trình, tóm tắt) |

```python
# Ví dụ gọi OpenAI để sinh bài tập
import openai

response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": "Bạn là trợ lý giáo dục..."},
        {"role": "user", "content": f"Tạo 5 câu hỏi trắc nghiệm từ nội dung: {content}"}
    ]
)
```

#### Tích hợp AWS S3

Mọi file upload đều được đẩy lên **AWS S3** bucket `Slothub-upload-2026`:

```python
import boto3

s3_client = boto3.client(
    's3',
    aws_access_key_id=os.getenv('AWS_ACCESS_KEY'),
    aws_secret_access_key=os.getenv('AWS_SECRET_KEY'),
    region_name='ap-southeast-1'
)

# Upload file
s3_client.upload_fileobj(
    file_obj,
    'Slothub-upload-2026',
    f'classrooms/{classroom_id}/{filename}'
)
```

#### Kết nối Database Trực tiếp

Khác với backend (dùng JPA/Hibernate), dịch vụ AI kết nối **trực tiếp** tới PostgreSQL qua `psycopg2`:

```python
import psycopg2

conn = psycopg2.connect(
    host=os.getenv('DB_HOST'),
    dbname=os.getenv('DB_NAME'),
    user=os.getenv('DB_USERNAME'),
    password=os.getenv('DB_PASSWORD')
)
```

{{% notice warning %}}
Dịch vụ AI **tự động chạy migration** khi khởi động — tạo các bảng riêng nếu chưa tồn tại (vd: bảng lưu embedding vectors). Đây là thiết kế có chủ đích để service có thể được deploy độc lập.
{{% /notice %}}

#### API Endpoints của AI Service

| Endpoint | Method | Mô tả |
|----------|--------|--------|
| `/api/v1/generate-exercises` | POST | Sinh bài tập từ tài liệu upload |
| `/api/v1/roadmap` | POST | Tạo lộ trình ôn tập cá nhân hóa |
| `/api/v1/upload` | POST | Upload file lên S3 |
| `/api/v1/chat/proxy` | POST | Chuyển tiếp tin nhắn chat tới Slozy |
| `/api/v1/subjects` | GET | Danh sách môn học |
| `/api/v1/books/{id}/content` | GET | Lấy nội dung sách/giáo trình |

#### Khởi chạy Dịch vụ AI

```bash
# Di chuyển vào thư mục AI
cd AI/

# Tạo virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Cài đặt dependencies
pip install -r requirements.txt

# Chạy server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

{{% notice info %}}
Flag `--reload` cho phép hot-reload khi thay đổi mã nguồn trong quá trình phát triển. Loại bỏ flag này trên môi trường production.
{{% /notice %}}

Phần tiếp theo sẽ khám phá **Agent-Core (Slozy)** — trí tuệ đằng sau gia sư AI, với LangGraph ReAct Agent và AWS Bedrock AgentCore.
