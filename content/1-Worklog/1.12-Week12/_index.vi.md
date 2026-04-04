---
title: "Worklog Tuần 12"
date: 2026-03-29
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---

### MỤC TIÊU TRONG WEEK 12:
- Thực hiện chuyển đổi (Migrate) hệ thống RAG từ môi trường phát triển lên hạ tầng AWS sử dụng các dịch vụ native (RDS PostgreSQL + pgvector, Amazon Bedrock).
- Áp dụng Infrastructure as Code (IaC) với Terraform để triển khai hạ tầng RAG một cách tự động và nhất quán.
- Làm chủ kỹ năng quản trị chi phí và tuân thủ (Governance) thông qua IAM Policy nâng cao (giới hạn Region, Instance Type).
- Thiết lập hệ thống giám sát toàn diện: Từ tầng mạng (VPC Flow Logs), tầng ứng dụng (Grafana) đến tầng dịch vụ AWS (CloudWatch).

### CÁC ĐẦU VIỆC CỦA WEEK 12:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Họp team project: Phát triển backend - RAG system (được kết hợp từ hybrid search engine và LLM):**<br>**- Nghiên cứu best practices về các dịch vụ AWS phục vụ cho RAG system**<br>**- Tiến hành migrate RAG system lên AWS** | 30/03/2026 | 30/03/2026 | [RDS PostgreSQL](https://aws.amazon.com/vi/rds/postgresql/)<br>[pgvector](https://github.com/pgvector/pgvector)<br>[Postgres Full Text](https://www.postgresql.org/docs/current/textsearch.html)<br>[Claude 3.5 Haiku](https://aws.amazon.com/vi/about-aws/whats-new/2024/11/anthropics-claude-3-5-haiku-model-amazon-bedrock/)<br>[Claude 3.5 Sonnet](https://aws.amazon.com/vi/about-aws/whats-new/2024/06/anthropic-claude-3-5-sonnet-model-bedrock/) |
| **3** | **- Thực hành Lab 30: Quản trị Chi phí và Sử dụng tài nguyên với IAM trên AWS**<br>+ Chuẩn bị<br>* Tạo IAM Group<br>* Tạo IAM user<br>+ Giới hạn theo Region<br>* Tạo policy giới hạn<br>* Gán policy vào group<br>* Kiểm tra hiệu quả policy<br>+ Giới hạn theo EC2 family<br>* Tạo policy giới hạn<br>* Gán policy vào group<br>* Kiểm tra hiệu quả policy<br>+ Giới hạn theo instance size<br>* Cập nhật policy giới hạn<br>* Kiểm tra hiệu quả policy<br>+ Giới hạn theo EBS volume<br>* Tạo policy giới hạn<br>* Gán policy vào group<br>* Kiểm tra hiệu quả policy<br>+ Dọn dẹp tài nguyên | 31/03/2026 | 31/03/2026 | [Lab 30 Intro](https://000064.awsstudygroup.com/vi/1-preparation/)<br>[Limit Region](https://000064.awsstudygroup.com/vi/2-limit-region/)<br>[Limit Family](https://000064.awsstudygroup.com/vi/3-limit-family/)<br>[Limit Size](https://000064.awsstudygroup.com/vi/4-limit-size/) |
| **4** | **- Thực hành Lab 31: Giám sát hạ tầng mạng với VPC Flow Log**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>+ Kích hoạt VPC Flow Logs<br>+ Giám sát hạ tầng mạng<br>+ Dọn dẹp tài nguyên<br>**- Thực hành Lab 32: Bắt đầu với Grafana trên AWS**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>* Tạo VPC và subnet<br>* Tạo Security Group<br>* Tạo EC2 Instance<br>* Tạo IAM User<br>* Tạo IAM Role<br>* Gán IAM Role<br>+ Cài đặt Grafana<br>+ Giám sát với Grafana<br>+ Dọn dẹp tài nguyên | 01/04/2026 | 01/04/2026 | [Lab 31 Intro](https://000074.awsstudygroup.com/vi/1-introduce/)<br>[VPC Flow Logs](https://000074.awsstudygroup.com/vi/4-enablevpcflowlogs/)<br>[Lab 32 Intro](https://000029.awsstudygroup.com/vi/1-introduce/)<br>[Install Grafana](https://000029.awsstudygroup.com/vi/3-installgrafana/) |
| **5** | **- Họp team project: Phát triển backend - RAG system (được kết hợp từ hybrid search engine và LLM):**<br>**- Hoàn thiện migrate RAG system lên AWS với Infrastructure as Code bằng TerraForm** | 02/04/2026 | 02/04/2026 | [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)<br>[Terraform CI/CD AWS](https://docs.aws.amazon.com/whitepapers/latest/cicd_for_5g_networks_on_aws/terraform.html)<br>[Terraform Tutorial](https://www.youtube.com/watch?v=wAwVOFf0Xq4) |
| **6** | **- Thực hành Lab 33: AWS CloudWatch Workshop**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>+ CloudWatch Metric<br>* Viewing Metrics<br>* Search expressions<br>* Math expressions<br>* Dynamic Labels<br>+ CloudWatch Logs<br>* CloudWatch Logs<br>* CloudWatch Logs Insights<br>* CloudWatch Metric Filter<br>+ CloudWatch Alarms<br>+ CloudWatch Dashboards<br>+ Dọn dẹp tài nguyên | 03/04/2026 | 03/04/2026 | [Lab 33 Intro](https://000036.awsstudygroup.com/vi/1-introduce/)<br>[Metrics](https://000036.awsstudygroup.com/vi/3-cloudwatchmetric/)<br>[Logs](https://000036.awsstudygroup.com/vi/4-cloudwatchlogs/)<br>[Alarms](https://000036.awsstudygroup.com/vi/5-cloudwatchalarm/) |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 12:
1. Di chuyển thành công hệ thống RAG lên AWS, sử dụng RDS PostgreSQL (pgvector) làm Vector Database và Amazon Bedrock (Claude Models) làm LLM.
2. Tự động hóa việc triển khai hạ tầng Backend RAG bằng Terraform, đảm bảo tính nhất quán và dễ dàng mở rộng.
3. Thiết lập các chính sách IAM chặt chẽ để kiểm soát việc tạo tài nguyên, ngăn chặn vượt ngân sách (Cost Control) và đảm bảo an ninh.
4. Xây dựng hệ thống giám sát đa tầng: Theo dõi lưu lượng mạng với VPC Flow Logs và trực quan hóa Metric ứng dụng trên Grafana/CloudWatch Dashboard.