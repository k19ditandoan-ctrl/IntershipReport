---
title: "Worklog Tuần 2"
date: 2026-01-11
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### MỤC TIÊU TRONG WEEK 2:
- Hiểu và thực hành quản lý truy cập người dùng an toàn với AWS IAM.
- Nắm vững kiến trúc mạng Amazon VPC và các lớp bảo mật mạng (Security Groups, NACL).
- Triển khai kết nối Hybrid Cloud thông qua AWS Site-to-Site VPN.
- Mở rộng kiến thức qua sự kiện cộng đồng và khởi động dự án nhóm.

### CÁC ĐẦU VIỆC CỦA WEEK 2:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Thực hành Lab 4: Quản trị quyền truy cập với AWS Identity and Access Management (IAM)**<br>+ IAM User và IAM Group<br>+ IAM Role<br>+ Chuyển đổi Role<br>**- Thực hành Lab 5: Bắt đầu với Amazon Virtual Private Cloud (VPC) và AWS Site-to-Site VPN**<br>+ Giới thiệu Amazon VPC:<br>* Subnets<br>* Route Table<br>* Internet Gateway<br>* NAT Gateway<br>+ Network Security với Security Groups và Network ACLs:<br>* Security groups<br>* Network ACLs<br>* VPC Resource Map | 12/01/2026 | 12/01/2026 | [Lab 4 Guide](https://000002.awsstudygroup.com/vi/)<br>[Lab 5 Intro](https://000003.awsstudygroup.com/vi/1-introduce/)<br>[Lab 5 Firewall](https://000003.awsstudygroup.com/vi/2-firewallinvpc/) |
| **3** | **- Tiếp tục thực hành Lab 5:**<br>+ Chuẩn bị Môi trường:<br>* Tạo VPC<br>* Tạo Subnet<br>* Tạo Internet Gateway<br>* Tạo Route Table<br>* Tạo Security Group<br>* Kích hoạt VPC Flow Logs<br>+ Triển khai Amazon EC2 Instance<br>* Tạo EC2 Instances<br>* Kiểm thử Phương thức Kết nối<br>* Tạo Multi-AZ NAT Gateway<br>* Sử dụng Reachability Analyzer<br>* Cấu hình EIC Endpoint<br>* AWS Systems Manager Session Manager<br>* CloudWatch Monitoring & Alerting | 13/01/2026 | 13/01/2026 | [Lab 5 Prerequisite](https://000003.awsstudygroup.com/vi/3-prerequisite/)<br>[Lab 5 Create EC2](https://000003.awsstudygroup.com/vi/4-createec2server/) |
| **4** | **- Tiếp tục thực hành Lab 5:**<br>+ Thiết lập AWS Site-to-Site VPN:<br>* Tạo môi trường VPN<br>Tạo VPC cho VPN<br>Tạo EC2 Instance<br>* Cấu hình kết nối VPN<br>Tạo Virtual Private Gateway<br>Tạo Customer Gateway<br>Tạo kết nối VPN<br>Cấu hình Customer Gateway<br>Tùy chỉnh AWS VPN Tunnel<br>Cấu hình VPN Nâng cao | 14/01/2026 | 14/01/2026 | [Lab 5 VPN](https://000003.awsstudygroup.com/vi/5-vpnsitetosite/) |
| **5** | **- Triển khai và thực hành với các dịch vụ mạng AWS (VPC, IGW, NAT Gateway)** | 15/01/2026 | 15/01/2026 | |
| **6** | **- Họp team project: lên ý tưởng, phân tích, nghiên cứu để chọn lọc idea phù hợp** | 16/01/2026 | 16/01/2026 | |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 2:
1. Hoàn thành Lab 4, thành thạo việc tạo IAM User, Group và Role để phân quyền truy cập hợp lý.
2. Xây dựng thành công hạ tầng mạng VPC với đầy đủ các thành phần: Subnet, Route Table, IGW, NAT Gateway.
3. Cấu hình bảo mật mạng nhiều lớp sử dụng Security Groups và Network ACLs.
4. Triển khai và giám sát EC2 Instance, cấu hình truy cập an toàn qua Session Manager và EIC Endpoint.
5. Thiết lập thành công kết nối AWS Site-to-Site VPN để kết nối giữa AWS và môi trường giả lập On-premise.