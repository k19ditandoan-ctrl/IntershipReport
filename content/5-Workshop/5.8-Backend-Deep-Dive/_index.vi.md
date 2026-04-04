---
title: "Backend Spring Boot"
date: 2026-04-03
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Tổng quan Backend

Backend của Slothub được xây dựng trên **Java 17 + Spring Boot 3.5**, đóng vai trò trung tâm xử lý logic nghiệp vụ giáo dục và là lớp API chính mà frontend giao tiếp. Dịch vụ này chạy trên cổng `8080` và kết nối trực tiếp đến cơ sở dữ liệu PostgreSQL (`EDU_CARE`).

#### Mô hình Domain chính

Hệ thống được thiết kế quanh các thực thể (entities) nghiệp vụ giáo dục, phân cấp rõ ràng:

##### Quản lý Người dùng
```
User (Cơ sở)
├── Teacher (Giáo viên)
└── Student (Học sinh)
```
- **User**: Thực thể gốc chứa thông tin xác thực (email, mật khẩu hash, vai trò).
- **Teacher**: Kế thừa từ User, có thể tạo lớp, giao bài, quản lý thời khóa biểu.
- **Student**: Kế thừa từ User, tham gia lớp, nộp bài, truy cập tài liệu.

##### Quản lý Lớp học
| Entity | Vai trò |
|--------|---------|
| `Classroom` | Thông tin lớp (tên, mã, giáo viên chủ nhiệm) |
| `ClassMember` | Mối quan hệ học sinh – lớp |
| `Timetable` | Thời khóa biểu theo lớp |
| `Attendance` | Điểm danh hàng ngày |

##### Quản lý Bài tập
| Entity | Vai trò |
|--------|---------|
| `Assignment` | Bài giao (đề bài, deadline, file đính kèm) |
| `Submission` | Bài nộp từ học sinh |
| `Question` | Câu hỏi đơn lẻ |
| `QuestionBank` | Ngân hàng câu hỏi theo môn/chủ đề |

##### Hệ thống Nội dung Phân cấp
```
Book (Sách)
└── Chapter (Chương)
    └── Section (Mục)
        └── Subsection (Tiểu mục)
            └── Lesson (Bài học)
```

Hệ thống nội dung phân cấp 5 tầng này cho phép tổ chức giáo trình một cách có cấu trúc, là nền tảng để AI agent truy vấn lý thuyết chính xác thông qua RAG.

##### Hỗ trợ AI & Tương tác
| Entity | Vai trò |
|--------|---------|
| `AIChatSession` | Phiên hội thoại với gia sư AI Slozy |
| `Roadmap` | Lộ trình ôn tập được tạo bởi AI |

#### Hệ thống Xác thực & Phân quyền

Slothub sử dụng **JWT (JSON Web Token)** kết hợp **Spring OAuth2 Resource Server** để bảo mật API:

```
Luồng xác thực:
1. Client gửi POST /auth/login với email + password
2. Backend xác minh credentials, tạo JWT token
3. JWT được ký bằng JWT_SIGNER_KEY (HMAC-SHA256)
4. Client lưu token vào localStorage
5. Mỗi request API kèm header: Authorization: Bearer <token>
6. Spring Security chặn và xác minh JWT tự động
```

##### Tính năng bảo mật nổi bật

- **Token Blacklist**: Khi người dùng logout, token bị đưa vào danh sách đen (blacklist) để vô hiệu hóa ngay lập tức, ngăn chặn việc sử dụng trái phép token còn hạn.
- **Reset mật khẩu qua Email**: Hệ thống gửi link reset mật khẩu qua **Gmail SMTP** khi người dùng quên mật khẩu.
- **Session Expiration**: Frontend lắng nghe sự kiện `Slothub:session-expired` (khi nhận HTTP 401) để tự động đăng xuất người dùng.

#### Cấu trúc Mã nguồn Backend

```text
backend/src/main/java/
├── config/           # Cấu hình Spring Security, CORS, JWT filter
├── controller/       # REST Controllers (Classroom, User, Assignment...)
├── dto/              # Data Transfer Objects (request/response)
├── entity/           # JPA Entities (ánh xạ thẳng tới bảng PostgreSQL)
├── exception/        # Xử lý ngoại lệ tập trung (GlobalExceptionHandler)
├── mapper/           # MapStruct mappers (Entity ↔ DTO)
├── repository/       # Spring Data JPA Repositories
└── service/          # Business Logic Layer
```

#### API Endpoints chính

| Nhóm | Endpoint | Method | Mô tả |
|------|----------|--------|--------|
| Auth | `/auth/login` | POST | Đăng nhập, nhận JWT token |
| Auth | `/auth/logout` | POST | Đăng xuất, blacklist token |
| Auth | `/auth/reset-password` | POST | Gửi email reset mật khẩu |
| User | `/api/users` | GET/POST | CRUD người dùng |
| Classroom | `/api/classrooms` | GET/POST | Quản lý lớp học |
| Assignment | `/api/assignments` | GET/POST | Giao và quản lý bài tập |
| Submission | `/api/submissions` | GET/POST | Nộp và chấm bài |
| Timetable | `/api/timetables` | GET/POST | Quản lý thời khóa biểu |
| Attendance | `/api/attendance` | GET/POST | Điểm danh |

#### Build & Chạy Backend

```bash
# Di chuyển tới thư mục backend
cd backend/

# Cài đặt dependencies và build
./mvnw clean install -DskipTests

# Chạy ứng dụng
./mvnw spring-boot:run
```

{{% notice info %}}
Backend sẽ tự động tạo schema database (DDL) khi khởi động lần đầu nhờ cấu hình `spring.jpa.hibernate.ddl-auto` trong `application.yml`. Đảm bảo PostgreSQL container đã chạy trước khi start Spring Boot.
{{% /notice %}}

Phần tiếp theo sẽ đi sâu vào dịch vụ AI (FastAPI) — nơi xử lý sinh nội dung giáo dục tự động và tương tác với các dịch vụ AI đám mây.
