---
title: "Worklog Tuần 6"
date: 2026-02-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### MỤC TIÊU TRONG WEEK 6:
- Hiểu và ứng dụng kiến trúc Serverless (AWS Lambda) để tự động hóa vận hành (Cost Optimization) và xử lý sự kiện (Event-driven).
- Nắm vững cách tương tác giữa Lambda với các dịch vụ lưu trữ (S3) và cơ sở dữ liệu NoSQL (DynamoDB).
- Làm chủ công cụ dòng lệnh AWS CLI để quản lý tài nguyên nhanh chóng và chuyên nghiệp thay vì chỉ dùng Console.
- Hoàn thiện thiết kế kiến trúc (Solution Architecture) và bảng ước tính chi phí (Budget Estimation) cho dự án nhóm.

### CÁC ĐẦU VIỆC CỦA WEEK 6:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Họp team project: Xác định, nghiên cứu solution architecture cho web app** | 09/02/2026 | 09/02/2026 | [Proposal Guide](https://workshop-sample.fcjuni.com/2-proposal/) |
| **3** | **- Thực hành Lab 13: Tối ưu chi phí EC2 với Lambda**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>* Tạo VPC<br>* Tạo Security Group<br>* Tạo EC2 instance<br>* Incoming Web-hooks slack<br>+ Tạo Tag cho Instance<br>+ Tạo Role cho Lambda<br>+ Tạo Lambda Function<br>* Function stop instance<br>* Function start instance<br>+ Kiểm tra kết quả<br>+ Dọn dẹp tài nguyên | 10/02/2026 | 10/02/2026 | [Lab 13 Intro](https://000022.awsstudygroup.com/vi/1-introduce/)<br>[Create Role](http://000022.awsstudygroup.com/vi/4-createroleforlambda/)<br>[Lambda Function](https://000022.awsstudygroup.com/vi/5-createlambdafunction/) |
| **4** | **- Thực hành Lab 14: Serverless - Tương tác giữa Lambda với S3 và DynamoDB**<br>+ Giới thiệu<br>+ Xử lý và Tối ưu Kích thước Ảnh trên AWS<br>* Tạo Lambda Function Xử Lý Ảnh<br>* Tạo S3 Bucket<br>* Tạo IAM Policy cho Lambda Function<br>* Kiểm tra hoạt động của Lambda Function<br>+ Ghi dữ liệu vào Amazon DynamoDB<br>* Tạo và Quản lý Bảng trong AWS DynamoDB<br>* Tạo Lambda Function để Ghi dữ liệu<br>+ Dọn dẹp tài nguyên | 11/02/2026 | 11/02/2026 | [Lab 14 Intro](https://000078.awsstudygroup.com/vi/1-introduce/)<br>[Resize Function](https://000078.awsstudygroup.com/vi/2-resize-image-function/)<br>[DynamoDB Write](https://000078.awsstudygroup.com/vi/3-write-data-to-dynaomodb/) |
| **5** | **- Tham gia workshop: Data Science on AWS - Mở khóa sức mạnh dữ liệu cùng điện toán đám mây**<br>**- Họp team project: Hoàn thiện solution architecture, budget estimation cho web app** | 12/02/2026 | 12/02/2026 | [AWS Calculator](https://calculator.aws/#/) |
| **6** | **- Thực hành Lab 15: Làm quen với AWS CLI**<br>+ Giới thiệu<br>+ Các bước chuẩn bị<br>+ Cài đặt AWS CLI<br>+ Kiểm tra tài nguyên qua CLI<br>+ AWS CLI với Amazon S3<br>+ AWS CLI với Amazon SNS<br>+ AWS CLI với IAM<br>+ AWS CLI với VPC<br>* AWS CLI với VPC<br>* AWS CLI với Internet Gateway<br>+ Tạo EC2 sử dụng AWS CLI<br>+ Khắc phục lỗi<br>+ Dọn dẹp tài nguyên | 13/02/2026 | 13/02/2026 | [Lab 15 Intro](https://000011.awsstudygroup.com/vi/1-introduce/)<br>[Install CLI](https://000011.awsstudygroup.com/vi/3-installcli/)<br>[CLI with EC2](https://000011.awsstudygroup.com/vi/9-ec2/) |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 6:
1. Triển khai thành công giải pháp tiết kiệm chi phí tự động (Lab 13): Sử dụng Lambda để Stop/Start EC2 theo lịch trình và tích hợp thông báo qua Slack.
2. Xây dựng ứng dụng Serverless xử lý ảnh (Lab 14): Kết hợp Lambda, S3 và DynamoDB để tự động resize ảnh và lưu metadata.
3. Hoàn thiện bản thiết kế kiến trúc (Solution Architecture) và bảng ước tính chi phí (Cost Estimation) chi tiết cho dự án cuối khóa.
4. Mở rộng kiến thức về Data Science trên nền tảng AWS thông qua workshop chuyên đề.
5. Sử dụng thành thạo AWS CLI (Lab 15) để thao tác với các dịch vụ cốt lõi (S3, EC2, VPC, IAM) mà không cần giao diện Console.