---
title: "Worklog Tuần 3"
date: 2026-01-18
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### MỤC TIÊU TRONG WEEK 3:
- Nắm vững kỹ năng xử lý sự cố (troubleshooting) VPN và mở rộng kết nối Site-to-Site với Transit Gateway.
- Hiểu và triển khai mô hình Hybrid DNS sử dụng Route 53 Resolver để phân giải tên miền giữa On-premise và AWS.
- Làm chủ các mô hình kết nối đa VPC (VPC Peering và Transit Gateway).
- Hệ thống hóa kiến thức chuyên sâu về dịch vụ Compute (EC2, AMI, EBS, Auto-scaling).

### CÁC ĐẦU VIỆC CỦA WEEK 3:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Tiếp tục thực hành Lab 5:**<br>+ Thiết lập AWS Site-to-Site VPN:<br>5.2 Cấu hình kết nối VPN:<br>5.2.7 Hướng dẫn Troubleshooting VPN<br>5.2.8 Hướng dẫn Troubleshooting VPN Chính thức từ AWS<br>5.3 Cấu hình VPN bằng strongSwan với Transit Gateway (Tùy chọn):<br>5.3.1 Tạo Customer Gateway<br>5.3.2 Tạo Transit Gateway<br>5.3.3 Tạo kết nối VPN<br>5.3.4 Tạo Transit Gateway Attachment<br>5.3.5 Cấu hình Route Tables<br>5.3.6 Cấu hình Customer Gateway<br>+ Dọn dẹp Tài nguyên<br>+ Infrastructure as Code Templates | 19/01/2026 | 19/01/2026 | [Lab 5 VPN](https://000003.awsstudygroup.com/vi/5-vpnsitetosite/) |
| **3** | **- Họp team project: Hoàn thiện idea, bổ sung thêm các tính năng dự kiến** | 20/01/2026 | 20/01/2026 | |
| **4** | **- Thực hành Lab 6: Thiết lập Hybrid DNS với Route 53 Resolver**<br>+ Các bước chuẩn bị:<br>* Tạo Key Pair<br>* Khởi tạo CloudFormation Template<br>* Cấu hình Security Group<br>+ Kết nối đến RDGW<br>+ Triển khai Microsoft AD<br>+ Thiết lập DNS:<br>* Tạo Route 53 Outbound Endpoint<br>* Tạo Route 53 Resolver Rules<br>* Tạo Route 53 Inbound Endpoints<br>* Thử nghiệm kết quả<br>+ Dọn dẹp tài nguyên | 21/01/2026 | 21/01/2026 | [Lab 6 Prereq](https://000010.awsstudygroup.com/vi/2-prerequiste/)<br>[Connect RDGW](https://000010.awsstudygroup.com/vi/3-connecttordgw/)<br>[Setup AD](https://000010.awsstudygroup.com/vi/4-setupad/)<br>[Hybrid DNS](https://000010.awsstudygroup.com/vi/5-setuphyriddns/) |
| **5** | **- Thực hành Lab 7: Thiết lập VPC Peering**<br>+ Các bước chuẩn bị:<br>* Khởi tạo CloudFormation Template<br>* Tạo Security Group<br>* Tạo EC2 instance<br>+ Cập nhật Network ACL<br>+ Tạo kết nối Peering<br>+ Kích hoạt Cross-Peer DNS<br>+ Dọn dẹp tài nguyên<br>**- Thực hành Lab 8: Tổng quan về AWS Transit Gateway**<br>+ Các bước chuẩn bị:<br>* Tạo Key Pair<br>* Khởi tạo CloudFormation Template<br>+ Tạo Transit Gateway<br>+ Tạo Transit Gateway Attachments<br>+ Tạo Transit Gateway Route Tables<br>+ Thêm Transit Gateway Routes vào VPC Route Tables<br>+ Dọn dẹp tài nguyên | 22/01/2026 | 22/01/2026 | [Lab 7 Guide](https://000019.awsstudygroup.com/vi/)<br>[Lab 8 Guide](https://000020.awsstudygroup.com/vi/) |
| **6** | **- Học Module 03: Compute VM on AWS:**<br>+ 03-01: EC2 Instance Types<br>+ 03-02: AMI, Backup, Key Pair<br>+ 03-03: Elastic Block Store (EBS)<br>+ 03-04: EC2 Instance Store<br>+ 03-05: EC2 User data<br>+ 03-06: EC2 Metadata<br>+ 03-07: EC2 Auto-scaling<br>+ EFS/FSx - Lightsail - MGN | 23/01/2026 | 23/01/2026 | [03-01](https://youtu.be/-t5h4N6vfBs?si=bS-jetOxckl24fDr)<br>[03-02](https://youtu.be/e7XeKdOVq40?si=c6LTJwwQ9vmc062Z)<br>[03-03](https://youtu.be/yAR6QRT3N1k?si=HmAky53nzXizTU8U)<br>[03-04](https://youtu.be/hKr_TfGP7NY?si=flt7IPIyoey3gp7D)<br>[03-05](https://youtu.be/6IHNDJ85aoQ?si=4oT7Yvm2MdgYM5dw)<br>[03-06](https://youtu.be/_v_43Wi7zjo?si=7UPcYjyhBr5NtpZM)<br>[03-07](https://youtu.be/Ew3QRaKJQSA?si=XPJt5rZRJIJaWkM4)<br>[Other](https://youtu.be/bbLcPitXJSY?si=gDfz13c9xm7z0cP2)<br>[MGN](https://youtu.be/hFVYG8WqfU0?si=pwMJL01CuoVoxMQS) |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 3:
1. Hoàn thành Lab 5 nâng cao: Biết cách Troubleshooting VPN và cấu hình VPN kết hợp với Transit Gateway (StrongSwan).
2. Thống nhất được ý tưởng cuối cùng cho dự án nhóm và xác định các tính năng cần triển khai.
3. Triển khai thành công kiến trúc Hybrid DNS (Lab 6), cấu hình Inbound/Outbound Endpoints để phân giải tên miền 2 chiều (AWS <-> On-prem).
4. Xây dựng và kết nối thành công các mạng VPC thông qua VPC Peering (Lab 7) và AWS Transit Gateway (Lab 8).
5. Nắm vững lý thuyết Module 03 về Compute: Hiểu sâu về các loại EC2, các loại ổ cứng EBS, và cơ chế Auto-scaling để tối ưu hóa hiệu suất và chi phí.