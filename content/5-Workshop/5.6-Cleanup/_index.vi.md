---
title: "Dọn dẹp"
date: 2026-04-03
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Dọn dẹp Tài nguyên & Kết thúc Dự án

Khi bạn đã hoàn thành việc quan sát cũng như test ứng dụng Slothub ở môi trường nội bộ, việc tắt hệ thống gọn gàng để trả lại tài nguyên máy chủ hay phòng hờ cước phí AWS phát sinh là cực kỳ quan trọng. Hãy làm theo trình tự:

##### 1. Đóng Các Trình Chạy Hệ Thống Local
Kiểm tra lại toàn bộ Terminal đang mở để chạy lệnh React, Spring Boot, FastAPI và Agent-Core, ấn tổ hợp `Ctrl+C` để giải phóng tất cả.

##### 2. Kết thúc Docker Compose Database
Chuyển tới thư mục có chứa cấu hình `docker-compose.yml`.
Nếu chỉ muốn tắt Container nhưng giữ lại Database (chuẩn bị chạy tiếp vào mai):
```bash
docker-compose stop
```
Trường hợp muốn xóa sạch cài đặt (Reset trắng toàn bộ Users và data Vector):
```bash
docker-compose down -v
```

##### 3. Lưu trữ Đám mây (AWS S3)
Xóa bỏ các tập tin và bài tập được tải lên để đảm bảo tài khoản AWS của bạn nằm trong Giới hạn Free Tier:
1. Truy cập **AWS Management Console**.
2. Tại dashboard **S3**, chọn chính xác tên bucket bạn đã trỏ (vd: `Slothub-upload-2026`).
3. Dùng chức năng "Empty bucket" và xác nhận.
4. (Tùy chọn) Bấm Xóa hoàn toàn ("Delete") Bucket đó khỏi tài khoản. 

##### 4. Loại bỏ AWS Bedrock Agent (Nếu có Deploy)
Trong trường hợp bạn tắt mode `LOCAL_DEV=1` đồng thời đẩy Trợ lý lên thẳng **AWS Bedrock AgentCore**:
1. Ở AWS Console, truy cập Amazon Bedrock.
2. Tại màn hình Agent, chọn Agent của bạn đang chạy.
3. Remove tất cả các bản nháp (Alias) và chọn Xóa (Delete Agent) để ngưng sử dụng Bedrock.

Thực hiện dọn dẹp cẩn thận giúp bạn tiết kiệm chi phí không đáng có từ những nguồn tài nguyên rác của AWS. Bài workshop Slothub (Slothub) tới đây xin được khép lại.
