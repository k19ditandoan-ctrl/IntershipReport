---
title: "Thiết lập Hạ tầng"
date: 2026-04-03
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Thiết lập Database Local

Vì các dịch vụ trong dự án yêu cầu giao tiếp liên tục với cơ sở dữ liệu PostgreSQL duy nhất (hỗ trợ phân tích vector cho AI), chúng ta đóng gói và thiết lập chúng qua một container nhằm đơn giản hóa môi trường phát triển (thay vì setup Database Cloud quá phức tạp).

1. Điều hướng đến thư mục gốc của project chứa file `docker-compose.yml`.
2. Đảm bảo ứng dụng Docker Desktop đã được mở.
3. Mở Terminal và thực thi lệnh:

    ```bash
    docker-compose up -d
    ```

4. Xác nhận rằng cả PostgreSQL (`:5432`) và pgAdmin (`:5050`) đều đã chạy.
5. Bạn có thể truy cập `http://localhost:5050` (Dùng tài khoản `admin@Slothub.com` / `admin`) để xem trực quan các bảng (tables) sau khi backend tự động khởi tạo dữ liệu mồi.

#### Thiết lập Lưu trữ Đám mây (AWS S3)

Để hệ thống có nơi lưu trữ các tệp tải lên (chẳng hạn tài liệu PDF) để phân tích ra lộ trình và tính điểm, chúng ta cần một bucket trên AWS S3.

1. Đăng nhập vào **AWS Management Console**.
2. Tìm kiếm và truy cập dịch vụ **S3**.
3. Bấm vào "Create bucket".
4. Nhập tên bucket không trùng lặp (vd: `Slothub-upload-2026`).
5. Lựa chọn khu vực thích hợp (vd: `ap-southeast-1`).
6. Bỏ chọn "Block all public access" nếu bạn muốn public URL hiển thị ảnh trực tiếp lên website (tùy thuộc kiến trúc, bạn có thể cân nhắc dùng Signed URLs và giữ public access nội bộ).
7. Nhấn "Create bucket".
8. Đảm bảo lấy được 2 chuỗi là `AWS_ACCESS_KEY_ID` và `AWS_SECRET_ACCESS_KEY` cho một tài khoản IAM có quyền truy cập vào Storage bucket này (`AmazonS3FullAccess`). Lưu trữ cẩn thận hai chuỗi chìa khóa trên.

#### Xác nhận Cấu hình

Với Database nội bộ PostgreSQL và khu vực lưu trữ Object storage S3 kết hợp, ta đã hoàn thành những bước đầu về Hạ tầng cho siêu ứng dụng Slothub. Giờ là lúc chạy từng Microservices trong bước Kế tiếp.
