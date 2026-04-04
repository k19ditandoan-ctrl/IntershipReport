---
title : "Giới thiệu"
date: 2026-04-03
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Về Slothub (Slothub)

**Slothub (Slothub)** là một nền tảng quản lý và học tập trực tuyến thông minh, được thiết kế nhằm đồng bộ trải nghiệm dạy và học. Nền tảng thay thế các công cụ rời rạc (sổ điểm, nhóm chat, tài liệu riêng lẻ) bằng một hệ sinh thái tất-cả-trong-một, được tối ưu hóa bởi Trí tuệ Nhân tạo.

Nền tảng sử dụng các công nghệ mạnh mẽ bao gồm:
- **AWS Bedrock AgentCore** - Vận hành **Trợ lý Slozy**, một gia sư AI hội thoại sử dụng kiến trúc LangGraph ReAct Agent và RAG (Retrieval-Augmented Generation) kết hợp với cơ sở dữ liệu PostgreSQL pgvector nhằm đảm bảo phản hồi chính xác dựa trên giáo trình.
- **OpenAI API** - Tự động phân tích tài liệu và sinh nội dung học tập (bài tập, lộ trình).
- **Amazon S3** - Lưu trữ bảo mật, có cấu trúc các tài liệu khóa học tải lên (PDF) và các tài sản được tạo ra.
- **Java Spring Boot** - Cung cấp REST API backend mạnh mẽ để quản lý logic giáo dục cốt lõi (lớp học, người dùng, bài tập, thời khóa biểu).

#### Tổng quan Workshop

Trong workshop này, bạn sẽ học cách khởi tạo, cấu hình và triển khai kiến trúc microservice của Slothub trên môi trường cục bộ (local):

- **Frontend (`frontend/`)**: React 18, TypeScript, Vite, Tailwind CSS. Thành phần này xử lý giao diện người dùng và tự động render (hiển thị) các widget trả về từ AI.
- **Backend (`backend/`)**: Spring Boot 3.5, Java 17. Quản lý xác thực (JWT/OAuth2) và xử lý dữ liệu người dùng, lớp học.
- **AI Service (`AI/`)**: Python 3.12, FastAPI. Chịu trách nhiệm tạo nội dung AI, upload file lên S3, và làm proxy kết nối đến model AI.
- **Agent-Core (`agent-core/`)**: Python 3.10, LangGraph. Trí tuệ của Trợ lý Slozy, chạy cục bộ với `MemorySaver` phục vụ mục đích test hoặc AWS Bedrock trên môi trường prod.
- **Cơ sở dữ liệu**: PostgreSQL với pgvector extension được chạy dễ dàng với **Docker Compose**.

#### Tóm tắt Kiến trúc

Slothub tuân theo phương pháp tiếp cận Microservice / Agentic AI:

1. **Tương tác của Người dùng**: Giao tiếp thông qua giao diện frontend React.
2. **Logic Cốt lõi**: Frontend gọi Spring Boot API để xác thực và lấy dữ liệu lớp học.
3. **Luồng Công việc AI**: Các yêu cầu sinh nội dung học tập được đẩy tới FastAPI, sau đó dịch vụ này sẽ gọi các OpenAI API và AWS S3.
4. **Gia sư Thông minh**: Học sinh nhắn tin với Slozy (Agent-Core / Bedrock) để truy xuất dữ liệu lý thuyết (RAG) từ bảng PostgreSQL pgvector.
5. **Tầng Dữ liệu**: Tất cả các dịch vụ kết nối chung tới một cơ sở dữ liệu PostgreSQL khởi tạo qua Docker Compose.

![Kiến trúc Slothub](/images/2-Proposal/Achitecture-Page-1.drawio.svg)
