---
title: "Worklog Tuần 10"
date: 2026-03-15
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### MỤC TIÊU TRONG WEEK 10:
- Nghiên cứu và thiết kế kiến trúc Backend hỗ trợ Hybrid Search (kết hợp tìm kiếm từ khóa và ngữ nghĩa) cho dự án.
- Làm chủ kiến trúc Serverless toàn diện: Từ xử lý sự kiện (S3 triggers), lưu trữ (DynamoDB) đến xây dựng API (API Gateway).
- Xây dựng quy trình CI/CD tự động cho ứng dụng Serverless bằng AWS CodePipeline.
- Thực hành giám sát (Monitoring) và truy vết (Tracing) ứng dụng Serverless chuyên sâu với CloudWatch và X-Ray.
- Mở rộng kết nối cộng đồng và tìm hiểu về Agentic AI.

### CÁC ĐẦU VIỆC CỦA WEEK 10:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Họp team project: Phát triển backend - Hybrid Search Engine (Text search + semantic search):**<br>- Nghiên cứu các best practices, paper về hybrid search engine<br>- Thiết kế kiến trúc sơ bộ hybrid search engine | 16/03/2026 | 16/03/2026 | [Paper](https://arxiv.org/pdf/2408.09236)<br>[Medium Article](https://medium.com/tech-learnings/hybrid-search-in-search-engines-bridging-the-gap-between-keywords-and-context-e8c5f6cabd6c)<br>[Meilisearch](https://www.meilisearch.com/blog/hybrid-search)<br>[Google Vertex AI](https://docs.cloud.google.com/vertex-ai/docs/vector-search/about-hybrid-search) |
| **3** | **- Thực hành Lab 22: Serverless - Tương tác giữa Lambda với S3 và DynamoDB**<br>+ Giới thiệu<br>+ Xử lý và Tối ưu Kích thước Ảnh trên AWS<br>* Tạo Lambda Function Xử Lý Ảnh<br>* Tạo S3 Bucket<br>* Tạo IAM Policy cho Lambda Function<br>* Kiểm tra hoạt động của Lambda Function<br>+ Ghi dữ liệu vào Amazon DynamoDB<br>* Tạo và Quản lý Bảng trong AWS DynamoDB<br>* Tạo Lambda Function để Ghi dữ liệu<br>+ Dọn dẹp tài nguyên | 17/03/2026 | 17/03/2026 | [Lab 22 Intro](https://000078.awsstudygroup.com/vi/1-introduce/)<br>[Resize Function](https://000078.awsstudygroup.com/vi/2-resize-image-function/)<br>[DynamoDB Write](https://000078.awsstudygroup.com/vi/3-write-data-to-dynaomodb/) |
| **4** | **- Thực hành Lab 23: Serverless - Hướng dẫn viết Front-end gọi API Gateway**<br>+ Giới thiệu API Gateway / DynamoDB<br>+ Triển khai front-end<br>+ Triển khai Lambda function<br>* Tạo bảng trong DynamoDB<br>* Triển khai Lambda function<br>Lambda function ghi dữ liệu<br>Lambda function đọc dữ liệu<br>Lambda function xoá dữ liệu<br>+ Thiết lập API Gateway<br>* Tạo các method<br>* Cài đặt và kích hoạt CORS<br>+ Kiểm tra API với Postman<br>+ Kiểm tra API với front-end<br>+ Dọn dẹp tài nguyên | 18/03/2026 | 18/03/2026 | [Lab 23 Intro](https://000079.awsstudygroup.com/vi/1-introduction/)<br>[Deploy Frontend](https://000079.awsstudygroup.com/vi/2-front-end-deployment/)<br>[API Gateway](https://000079.awsstudygroup.com/vi/4-config-api-gw/)<br>[Postman Test](https://000079.awsstudygroup.com/vi/5-test-api-by-postman/) |
| **5** | **- Họp team project: Phát triển backend - Hybrid Search Engine (Text search + semantic search):**<br>- Chạy, kiểm thử hybrid search engine với data đã thu thập<br>- Hoàn thiện kiến trúc hybrid search engine | 19/03/2026 | 19/03/2026 | [Supabase AI](https://supabase.com/docs/guides/ai/hybrid-search)<br>[MongoDB Hybrid](https://www.mongodb.com/resources/products/capabilities/hybrid-search)<br>[AWS OpenSearch](https://aws.amazon.com/vi/blogs/big-data/hybrid-search-with-amazon-opensearch-service/)<br>[Amazon Bedrock](https://aws.amazon.com/vi/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-hybrid-search/) |
| **6** | **- Thực hành Lab 24: Serverless - CI/CD với CodePipeline**<br>+ Chuẩn bị<br>+ Xây dựng pipeline SAM<br>* Tạo kho Git<br>* Tạo SAM pipeline<br>+ Xây dựng pipeline cho front-end<br>* Tạo kho Git<br>* Tạo pipeline<br>+ Kiểm tra hoạt động web<br>+ Dọn dẹp<br>**- Thực hành Lab 25: Serverless - Giám sát ứng dụng Serverless với CloudWatch và X-Ray**<br>+ Chuẩn bị<br>+ Giám sát với CloudWatch<br>* Gỡ lỗi với nhật ký CloudWatch<br>* Tạo số liệu tùy chỉnh<br>* Tạo cảnh báo với CloudWatch Alarm<br>+ Theo dõi với X-ray<br>+ Dọn dẹp | 20/03/2026 | 20/03/2026 | [Lab 24 Intro](https://000084.awsstudygroup.com/vi/1-preparation/)<br>[SAM Pipeline](https://000084.awsstudygroup.com/vi/2-build-sam-pipeline/)<br>[Lab 25 Intro](https://000085.awsstudygroup.com/vi/1-preparation/)<br>[CloudWatch](https://000085.awsstudygroup.com/vi/2-cloudwatch-monitor/)<br>[X-Ray](https://000085.awsstudygroup.com/vi/3-x-ray-trace/) |
| **7** | **- Tham gia event: AWS Community Day Vietnam** | 21/03/2026 | 21/03/2026 | [Event Info](https://aws-community-day-vietnam-2025.awsstudygroup.com/) |

### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 10:
1. Thiết kế và kiểm thử thành công kiến trúc Hybrid Search Engine, kết hợp sức mạnh của tìm kiếm từ khóa truyền thống và tìm kiếm vector (Semantic).
2. Xây dựng hoàn chỉnh luồng xử lý Serverless Backend: Tự động hóa xử lý ảnh với S3 Trigger và quản lý dữ liệu NoSQL với DynamoDB.
3. Triển khai thành công Full-stack Serverless App: Kết nối Frontend với Backend thông qua API Gateway và Lambda, xử lý tốt vấn đề CORS.
4. Thiết lập quy trình DevOps tự động (CI/CD) cho ứng dụng Serverless, giúp việc deploy Code và Frontend trở nên nhanh chóng và ít lỗi.
5. Nâng cao khả năng vận hành hệ thống thông qua việc thiết lập Dashboard giám sát (CloudWatch) và truy vết luồng đi của request (X-Ray) để debug hiệu quả.