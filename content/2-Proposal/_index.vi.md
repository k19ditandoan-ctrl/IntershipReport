---
title: "Proposal"
date: "2026-04-03"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# SLOTHUB — Nền tảng hỗ trợ học tập và giảng dạy cho giáo viên và học sinh
*(Quản lý lớp học, bài tập, lịch học, tài liệu và trợ lý AI tích hợp Amazon Bedrock)*

---

## 1. Tóm tắt chung

**Slothub** là một hệ thống web hướng tới giáo viên, học sinh và quản trị viên, nhằm đồng bộ hoạt động dạy–học trên một nền tảng duy nhất: từ quản lý lớp, thời khóa biểu, điểm danh, giao và chấm bài, đến tài liệu, thông báo và **trợ lý học tập thông minh** (gợi ý lộ trình ôn tập, trắc nghiệm, trả lời theo kiến thức trong cơ sở dữ liệu giáo trình). Dự án được triển khai theo hướng **đám mây AWS** tại khu vực **ap-southeast-1 (Singapore)** với thiết kế **đa vùng sẵn sàng (Multi-AZ)** nhằm tăng tính sẵn sàng và khả năng phục hồi.

**Frontend** được xây dựng bằng **React, TypeScript và Vite**, giao diện responsive, hỗ trợ đa ngôn ngữ (vi/en). **Backend** dùng **Java Spring Boot** (REST API, bảo mật OAuth2/JWT), kết nối **Amazon RDS for PostgreSQL** cho dữ liệu quan hệ (người dùng, lớp, bài giao, bài nộp, thời khóa biểu, điểm danh, phiên chat…). **Dịch vụ AI** gồm một **API FastAPI** (Python) xử lý sinh đề, lộ trình, trích xuất tài liệu, tích hợp **Amazon S3** cho tệp tài liệu; và **Amazon Bedrock AgentCore** triển khai agent **gia sư AI (Slozy)** với các công cụ tìm kiếm lý thuyết (vector trên PostgreSQL), gợi ý lộ trình và quiz — phù hợp với kiến trúc “Fargate Backend + Fargate AI” và **Amazon Bedrock** trong sơ đồ hệ thống.

Mục tiêu là giảm thiểu gánh nặng quản trị hành chính cho giáo viên, giúp học sinh chủ động ôn tập có định hướng, đồng thời tận dụng các dịch vụ AWS (Cognito, WAF, Amplify, ALB, Fargate, ECR, RDS, S3, Bedrock, CloudWatch, GuardDuty…) để triển khai và vận hành có kiểm soát.

---

## 2. Phát biểu vấn đề

### Vấn đề là gì?

- **Công cụ rời rạc**: Giáo viên thường phải dùng nhiều công cụ rời (bảng điểm, nhóm chat, file tài liệu, form bài tập), dễ mất thời gian và thiếu nhất quán dữ liệu.
- **Thiếu tính cá nhân hóa**: Học sinh khó theo dõi tiến độ, lịch học và bài tập; thiếu phản hồi cá nhân hóa kịp thời ngoài giờ lên lớp.
- **AI chưa được kiểm soát**: Các nền tảng học tập truyền thống ít tích hợp **AI an toàn** trong ngữ cảnh giáo dục (hướng dẫn từng bước, không hallucination).
- **Yêu cầu vận hành**: Đòi hỏi hệ thống có tính **bảo mật, mở rộng và khả dụng cao** khi triển khai thực tế.

### Giải pháp

Slothub tập trung dữ liệu và quy trình trên một stack thống nhất: API Spring Boot + PostgreSQL RDS; dịch vụ AI tách riêng (container) gọi mô hình **Amazon Bedrock** và lưu trữ tài liệu trên **S3**; trợ lý gia sư **AgentCore** truy vấn nội dung lý thuyết từ cơ sở dữ liệu (RAG - tìm kiếm vector) thay vì “bịa” kiến thức. Người dùng xác thực qua **Amazon Cognito**; truy cập qua **WAF**, **AWS Amplify** (hosting frontend) và **ALB** phân phối tới **AWS Fargate**; cơ sở dữ liệu **RDS PostgreSQL** chạy chế độ **Multi-AZ**.

### Lợi ích và ROI

- **Tập trung**: Đồng nhất lộ trình học tập, quản lý lớp, thời khóa biểu và bài tập.
- **Cá nhân hóa**: Lộ trình ôn tập, quiz và chat gia sư hỗ trợ theo từng môn/ngữ cảnh.
- **Tin cậy vận hành**: Multi-AZ cho RDS, Fargate trải trên nhiều AZ, giám sát **CloudWatch**, bảo mật **GuardDuty**.
- **Khả năng mở rộng**: Container hóa, dễ dàng mở rộng độc lập giữa dịch vụ AI và backend.
- **Kiểm soát chi phí**: Tối ưu theo tần suất sử dụng (Fargate, Bedrock) và caching.

---

## 3. Kiến trúc giải pháp

### Tổng quan

Luồng chính: **Người dùng → Cognito (xác thực) → ALB → Fargate (Backend hoặc AI)**; dữ liệu lưu tại **RDS PostgreSQL (Multi-AZ)** và tệp tại **S3 (documents bucket)**; dịch vụ AI tương tác **Amazon Bedrock (AgentCore)**.

![Kiến trúc giải pháp Slothub](/images/2-Proposal/Achitecture-Page-1.drawio.svg)

### Dịch vụ AWS được sử dụng

| Dịch vụ | Vai trò |
|--------|---------|
| **Amazon Cognito** | Xác thực và phân quyền người dùng |
| **Amazon Route 53** | DNS và định tuyến tên miền |
| **AWS WAF** | Bảo vệ ứng dụng web khỏi các khai thác phổ biến |
| **AWS Amplify** | Hosting và quản lý frontend |
| **AWS Certificate Manager** | Quản lý chứng chỉ SSL/TLS |
| **Amazon VPC + IGW** | Mạng riêng, kết nối internet có kiểm soát |
| **Application Load Balancer** | Cân bằng tải tới các dịch vụ container |
| **Amazon ECS on Fargate** | Chạy Spring Boot và FastAPI không quản lý server |
| **Amazon ECR** | Lưu trữ Docker image cho backend và AI |
| **Amazon RDS (PostgreSQL)** | Cơ sở dữ liệu quan hệ Multi-AZ (Primary/Standby) |
| **Amazon S3** | Lưu trữ tài liệu khóa học và tệp đính kèm |
| **Amazon Bedrock (AgentCore)** | Triển khai Agent gia sư AI (Slozy) và LLM |
| **Amazon CloudWatch** | Ghi log và giám sát tài nguyên |
| **Amazon GuardDuty** | Phát hiện mối đe dọa bảo mật thông minh |

---

## 4. Triển khai kỹ thuật

### Các giai đoạn triển khai

| Giai đoạn | Nội dung | Thời gian gợi ý |
|-----------|----------|------------------|
| 1 | Chuẩn hóa kiến trúc AWS (VPC, ALB, Fargate, ECR, RDS Multi-AZ, Cognito, S3), IaC/CI cơ bản | 2–3 tuần |
| 2 | Hoàn thiện schema RDS, phát triển API Spring Boot và tích hợp Cognito | 3–4 tuần |
| 3 | Triển khai dịch vụ AI (FastAPI), pipeline S3, kết nối Bedrock | 2–3 tuần |
| 4 | Triển khai AgentCore (Slozy), nối công cụ tới PostgreSQL và API AI | 2 tuần |
| 5 | Build production frontend, triển khai Amplify, WAF, Route 53 | 2 tuần |
| 6 | Kiểm thử tải, giám sát CloudWatch, tinh chỉnh chi phí và bảo mật | 1–2 tuần |

### Yêu cầu kỹ thuật

- **Phía máy khách**: Trình duyệt hiện đại; giao diện responsive.
- **Backend**: Java 17, Spring Boot 3.x, PostgreSQL, Spring Security.
- **AI & Agent**: Python 3.x, FastAPI, Bedrock AgentCore SDK, LangGraph.
- **CI/CD**: GitHub Actions build Docker image, push ECR, cập nhật ECS Fargate.

---

## 5. Lịch trình và cột mốc

| Giai đoạn | Hoạt động |
|-----------|-----------|
| Chuẩn bị | Thống nhất ERD, API, quyền vai trò (giáo viên, học sinh, admin) |
| Phát triển lõi | Lớp học, bài tập, lịch trực tuyến, điểm danh và quản lý người dùng |
| Tích hợp AI | FastAPI + S3 + Bedrock; Triển khai Agent Slozy |
| Triển khai | ECR, Fargate, ALB, Amplify, Cognito, WAF |
| Vận hành | Giám sát hệ thống, backup RDS, xử lý sự cố |

---

## 6. Ước tính ngân sách

### Thời gian đầu tư (tham khảo)

Tổng giờ làm việc ước tính cho nhóm 5 thành viên (20 giờ/tuần) qua các giai đoạn là khoảng **600 giờ**.

### Chi phí đám mây

- **Tối ưu hóa**: Toàn bộ dự án được thiết kế để vận hành trong phạm vi ngân sách **$200 tín dụng từ AWS**.
- **Hạng mục**: Chi phí chính nằm ở RDS Multi-AZ, Fargate tasks và token sử dụng cho Bedrock.

---

## 7. Đánh giá rủi ro

| Rủi ro | Mức độ ảnh hưởng | Khả năng | Giải pháp giảm thiểu |
|--------|------------------|----------|------------|
| Lỗi đồng bộ dữ liệu Backend-AI | Cao | Trung bình | Định nghĩa API contract chặt chẽ, xử lý giao dịch rõ ràng |
| Chi phí Bedrock vượt dự kiến | Cao | Trung bình | Giới hạn quota, sử dụng bộ nhớ đệm (cache) |
| Sự cố RDS (failover) | Cao | Thấp | Cấu hình Multi-AZ, backup tự động |
| Bảo mật API/S3 | Cao | Trung bình | IAM least privilege, WAF, GuardDuty |
| Chất lượng phản hồi AI | Trung bình | Trung bình | Prompt engineering, kiểm duyệt nội dung dựa trên tri thức curriculum |

---

## 8. Kết quả dự kiến

### Tiêu chí thành công

- Triển khai **end-to-end** theo kiến trúc AWS hoàn chỉnh: Cognito, ALB, Fargate, RDS PostgreSQL Multi-AZ, S3, Bedrock AgentCore.
- **MVP** cho phép: quản lý lớp, giao bài, nộp bài, lịch/điểm danh và ít nhất một tính năng AI (Slozy AI Tutor hoặc Roadmap/Quiz).
- **An toàn**: Toàn bộ giao tiếp qua HTTPS, tích hợp WAF, log tập trung CloudWatch.
- **Hiệu quả**: Hệ thống AI phản hồi chính xác (>90% câu hỏi lý thuyết curriculum) thông qua RAG.

### Giá trị dài hạn

- Khả năng mở rộng thành hệ thống đa trường (Multi-tenancy).
- Chuyển đổi từ quản lý hành chính sang học thuật bổ trợ bởi trí tuệ nhân tạo.

---

## 9. Tài liệu tham khảo

- [AWS Pricing Calculator](https://calculator.aws/)
- Tài liệu Amazon Bedrock AgentCore và Amazon ECS Fargate.
- Mã nguồn dự án: thư mục `frontend`, `backend`, `AI`, `agent-core`.
