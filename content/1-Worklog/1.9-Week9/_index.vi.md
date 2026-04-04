---
title: "Worklog Tuần 9"
date: 2026-03-08
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### MỤC TIÊU TRONG WEEK 9:
- Tiếp cận và làm chủ AWS Cloud Development Kit (CDK) để định nghĩa hạ tầng đám mây bằng ngôn ngữ lập trình.
- Thực hành triển khai các kiến trúc phức tạp (ECS, ALB, API Gateway, Serverless) sử dụng CDK và Nested Stacks.
- Củng cố tư duy Infrastructure as Code (IaC) thông qua việc triển khai kiến trúc 3 tầng (Three-Tier Architecture) hoàn chỉnh.
- Hoàn tất giai đoạn chuẩn bị dữ liệu và thiết kế (Database/UI) cho dự án nhóm.
- Nâng cao kiến thức về LLM và Prompt Engineering thông qua các sự kiện cộng đồng.

### CÁC ĐẦU VIỆC CỦA WEEK 9:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Họp team project: Hoàn thiện thiết kế database, tiếp tục thu thập data** | 09/03/2026 | 09/03/2026 | |
| **3** | **- Thực hành Lab 19: CDK cơ bản**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>* Tạo IAM Role<br>+ CDK cơ bản<br>* Tạo workspace<br>* Cấu hình Cloud9<br>+ Tạo CDK Template<br>+ Cập nhật CDK Template<br>+ Dọn dẹp tài nguyên | 10/03/2026 | 10/03/2026 | [Lab 19 Intro](https://000038.awsstudygroup.com/vi/1-introduce/)<br>[CDK Basic](https://000038.awsstudygroup.com/vi/3-cdkbasic/)<br>[Create Template](https://000038.awsstudygroup.com/vi/4-createcdktemplate/) |
| **4** | **- Thực hành Lab 20: CDK Cơ bản - 2**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>* Tạo IAM Role<br>* Chạy một máy chủ EC2<br>* Cấu hình môi trường VSCode<br>+ ECS, ALB và API Gateway<br>+ Lambda và S3<br>+ Nested stack<br>* Tạo các stack lồng với CDK<br>+ Dọn dẹp tài nguyên | 11/03/2026 | 11/03/2026 | [Lab 20 Intro](https://000076.awsstudygroup.com/vi/1-introduction/)<br>[ECS & ALB](https://000076.awsstudygroup.com/vi/3-ecs-alb-and-api-gateway/)<br>[Nested Stack](https://000076.awsstudygroup.com/vi/5-nested-stack/) |
| **5** | **- Họp team project: Hoàn tất thu thập data, feedback cải thiện thiết kế UI figma** | 12/03/2026 | 12/03/2026 | |
| **6** | **- Thực hành Lab 21: Giới Thiệu về Infrastructure as Code**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>+ Tạo Lambda function<br>+ Tạo VPC và EC2<br>+ Triển khai Three-Tier Architecture<br>* Triển khai CloudFormation Stack<br>* Kiểm tra truy cập Web Tier<br>* Kiểm tra truy cập Application Tier<br>* Kiểm tra truy cập Database Tier<br>+ Dọn dẹp tài nguyên | 13/03/2026 | 13/03/2026 | [Lab 21 Intro](https://000102.awsstudygroup.com/vi/1-introduction/)<br>[Create Lambda](https://000102.awsstudygroup.com/vi/3-createlambda/)<br>[Three Tier](https://000102.awsstudygroup.com/vi/5-threetierweb/) |
| **7** | **- Tham gia event: Cloud Mastery — Automated Prompt Engineering: Enhancing LLM Output Quality** | 14/03/2026 | 14/03/2026 | |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 9:
1. Thiết lập thành công môi trường làm việc CDK (Cloud9, VSCode) và triển khai các Template hạ tầng cơ bản.
2. Ứng dụng CDK để xây dựng các tài nguyên nâng cao: ECS Cluster, Application Load Balancer, API Gateway và cấu trúc Nested Stack.
3. Triển khai thành công kiến trúc Three-Tier chuẩn mực (Web, App, Database layers) hoàn toàn bằng mã nguồn (IaC).
4. Hoàn thành mốc quan trọng của dự án nhóm: Chốt thiết kế Database, UI trên Figma và hoàn tất bộ dữ liệu cần thiết.