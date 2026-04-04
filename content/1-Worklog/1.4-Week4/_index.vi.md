---
title: "Worklog Tuần 4"
date: 2026-01-25
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### MỤC TIÊU TRONG WEEK 4:
- Làm chủ dịch vụ Amazon EC2: Quản lý vòng đời Instance, tạo Custom AMI, xử lý sự cố (Troubleshooting) và phục hồi dữ liệu.
- Thực hành triển khai ứng dụng Web thực tế (LAMP stack, Node.js) trên cả môi trường Linux và Windows.
- Hiểu sâu về các dịch vụ lưu trữ (S3, Storage Gateway) và mô hình bảo mật chia sẻ (Shared Responsibility Model).
- Nắm vững các dịch vụ bảo mật cốt lõi: IAM, Cognito, AWS Organization và KMS.

### CÁC ĐẦU VIỆC CỦA WEEK 4:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Thực hành Lab 9: Amazon Elastic Compute Cloud (EC2)**<br>+ Giới thiệu<br>+ Các bước chuẩn bị:<br>* Tạo VPC Linux<br>* Tạo VPC Windows<br>* Tạo Security Group Linux<br>* Tạo Security Group Windows<br>+ Khởi tạo Windows instance<br>* Tạo Windows Instance<br>* Kết nối Windows instance<br>+ Khởi tạo Linux instance<br>* Tạo Linux instance<br>* Kết nối Linux instance<br>+ Amazon EC2 cơ bản<br>* Thay đổi cấu hình EC2<br>* Tạo EC2 snapshot<br>* Tạo Custom AMI<br>* Tạo instance từ custom AMI<br>* Truy cập khi mất Key Pair EC2-Windows bằng SSM<br>* Truy cập khi mất Key Pair EC2-Linux bằng User Data<br>* Cấu hình giao diện Desktop cho EC2-Ubuntu 22.04<br>* Amazon EBS Snapshots Archive<br>* Chia sẻ AMI | 26/01/2026 | 26/01/2026 | [Lab 9 Intro](https://000004.awsstudygroup.com/vi/1-introduce/)<br>[Lab 9 Prereq](https://000004.awsstudygroup.com/vi/2-prerequiste/)<br>[Launch Windows](https://000004.awsstudygroup.com/vi/3-launchwindowsinstance/)<br>[Launch Linux](https://000004.awsstudygroup.com/vi/4-launchlinuxinstance/)<br>[EC2 Basic](https://000004.awsstudygroup.com/vi/5-amazonec2basic/) |
| **3** | **- Tiếp tục Lab 9:**<br>+ Triển khai ứng dụng Node.js trên Amazon Linux<br>* Cài đặt LAMP web server (Chuẩn bị, Kiểm tra, Cấu hình DB, cài đặt phpMyAdmin)<br>* Cài đặt Node.js trên Linux<br>* Triển khai ứng dụng trên Linux Instance<br>+ Ứng dụng Node.js trên Amazon EC2 Windows<br>* Cài đặt XAMPP trên Windows instance<br>* Cài đặt Nodejs trên Windows instance<br>* Triển khai ứng dụng trên Windows instance<br>+ Giới hạn sử dụng tài nguyên bằng dịch vụ IAM<br>* Cho phép sử dụng dịch vụ theo Region cụ thể<br>* Giới hạn sử dụng EC2 theo Instance Family<br>* Giới hạn sử dụng EC2 theo Instance type<br>* Giới hạn sử dụng EBS volume storage type<br>* Giới hạn quyền xóa tài nguyên theo địa chỉ IP của Doanh nghiệp<br>* Giới hạn quyền xóa tài nguyên theo khoảng thời gian<br>+ Dọn dẹp tài nguyên | 27/01/2026 | 27/01/2026 | [Linux App](https://000004.awsstudygroup.com/vi/6-awsfcjmanagement-linux/)<br>[Windows App](https://000004.awsstudygroup.com/vi/7-awsfcjmanagement-windows/)<br>[Governance](https://000004.awsstudygroup.com/vi/8-costusagegovernance/)<br>[Cleanup](https://000004.awsstudygroup.com/vi/9-cleanup/) |
| **4** | **- Học Module 04: Dịch vụ lưu trữ trên AWS:**<br>+ 04-01: Amazon Simple Storage Service ( S3 ) - Access Point - Storage Class<br>+ 04-02: S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier<br>+ 04-03: Snow Family - Storage Gateway - Backup | 28/01/2026 | 28/01/2026 | [04-01](https://youtu.be/_yunukwcAwc?si=6HqDHVQJq8Ks9aWh)<br>[04-02](https://youtu.be/mPBjB6Ltl_Q?si=OITIt1x3d7OZ4ei_)<br>[04-03](https://www.youtube.com/watch?v=YXn8Q_Hpsu4) |
| **5** | **- Tham gia event: AWS re:Invent re:Cap Vietnam — HCMC 2025** | 29/01/2026 | 29/01/2026 | |
| **6** | **- Học Module 05: Dịch vụ bảo mật trên AWS:**<br>+ 05-01: Share Responsibility Model<br>+ 05-02: Amazon Identity and access management<br>+ 05-03: Amazon Cognito<br>+ 05-04: AWS Organization<br>+ 05-05: AWS Identity Center<br>+ 05-06: Amazon Key Management Service<br>+ 05-07: AWS Security Hub | 30/01/2026 | 30/01/2026 | [05-01](https://youtu.be/tsobAlSg19g?si=-xSAVT8MZReV10RP)<br>[05-02](https://youtu.be/N_vlJGAqZxo?si=KxeWofBCdviRYax1)<br>[05-03](https://youtu.be/pZ2fgEFK3Vs?si=QWkbW4avA9wlvlhP)<br>[05-04](https://youtu.be/5oQY8Rogz9Y?si=WK72gwmztbXWQVKr)<br>[05-05](https://youtu.be/NW1xrMkNMjU?si=Owp-3CDDmW7YYTY4)<br>[05-06](https://youtu.be/GMihNQojhZc?si=Bt4oUqD2a5_IA0mm)<br>[05-07](https://youtu.be/clj2E0rNBEs?si=eUp1O-14XFDbpbbe) |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 4:
1. Hoàn thành toàn diện Lab 9: Thành thạo các tác vụ quản trị EC2 nâng cao (Resize, Snapshot, Custom AMI, Recovery Access).
2. Triển khai thành công ứng dụng thực tế (LAMP Stack, Node.js) trên hạ tầng EC2 Linux và Windows.
3. Thực hành quản trị chi phí và tuân thủ (Governance) bằng cách giới hạn quyền tạo tài nguyên theo Region, Instance Type và thời gian thông qua IAM Policy.
4. Nắm vững kiến thức Module 04 về các giải pháp lưu trữ dữ liệu (S3, Glacier, Storage Gateway) và chiến lược sao lưu (Backup).
5. Hệ thống hóa kiến thức Module 05 về bảo mật đám mây, hiểu rõ mô hình trách nhiệm chia sẻ và cách sử dụng các công cụ bảo mật Identity (IAM, Cognito, Identity Center).