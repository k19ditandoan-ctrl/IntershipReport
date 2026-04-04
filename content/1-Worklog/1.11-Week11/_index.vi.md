---
title: "Worklog Tuần 11"
date: 2026-03-22
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### MỤC TIÊU TRONG WEEK 11:
- Nâng cấp Hybrid Search Engine bằng cách tích hợp LLM để xây dựng hệ thống RAG (Retrieval-Augmented Generation) hoàn chỉnh.
- Làm chủ quy trình phát triển ứng dụng Serverless phức tạp (Frontend, Backend, Xử lý ảnh) sử dụng AWS SAM.
- Thực hành quy trình Machine Learning chuyên nghiệp trên Amazon SageMaker: Từ Feature Engineering đến Deploy Model.
- Tối ưu hóa hiệu suất lập trình với bộ công cụ AI của AWS (Amazon Q, CodeWhisperer) trên VS Code.

### CÁC ĐẦU VIỆC CỦA WEEK 11:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|:---:|---|:---:|:---:|---|
| **2** | **- Họp team project: Phát triển backend - Hybrid Search Engine (Text search + semantic search):**<br>- Cải thiện độ chính xác của hybrid search engine với LLM<br>- Bổ sung tính năng chat với user để tìm kiếm thay vì chỉ tìm kiếm thông thường<br>- Nghiên cứu về các best practices, paper cho hệ thống RAG | 23/03/2026 | 23/03/2026 | [RAG Paper 1](https://arxiv.org/pdf/2509.13603)<br>[RAG Paper 2](https://arxiv.org/pdf/2508.18048)<br>[Meilisearch Hybrid](https://www.meilisearch.com/blog/fixing-hybrid-search)<br>[Elastic RAG](https://www.elastic.co/search-labs/blog/llm-agents-intelligent-hybrid-search) |
| **3** | **- Thực hành Lab 26: Serverless - Hướng dẫn viết Front-end gọi API Gateway**<br>+ Triển Khai Front-end<br>+ Thiết Lập API Gateway<br>+ Kiểm Tra API Với Postman<br>+ Kiểm Tra API Với Front-end<br>+ Dọn Dẹp Tài Nguyên<br>**- Thực hành Lab 27: Serverless với Lambda, API Gateway và SAM**<br>+ Giới thiệu<br>+ Chuẩn bị<br>* Tạo Cloud9 instance<br>* Tạo CodeCommit Repository<br>+ Triển khai ứng dụng mẫu<br>* Triển khai Frontend<br>* Triển khai Backend<br>Triển khai hạ tầng<br>Điền thông tin chuyến đi<br>Kiểm tra cấu hình<br>* Cập nhật Frontend<br>+ Triển khai ride times system<br>* Triển khai Backend<br>* Triển khai Frontend<br>+ Xử lý ảnh trên xe<br>* Triển khai Backend<br>Tạo Chroma Key Lambda function<br>Tạo Photo-Compositing Lambda function<br>Post-processing<br>* Kiểm tra tính năng<br>+ Dọn dẹp tài nguyên | 24/03/2026 | 24/03/2026 | [Lab 26 Intro](https://000135.awsstudygroup.com/vi/1-front-end-deployment/)<br>[API Gateway](https://000135.awsstudygroup.com/vi/2-config-api-gw/)<br>[Lab 27 Intro](https://000066.awsstudygroup.com/vi/1-introduce/)<br>[Deploy App](https://000066.awsstudygroup.com/vi/3-deployapp/)<br>[Image Processing](https://000066.awsstudygroup.com/vi/5-on-ridesphotoprocessing/) |
| **4** | **- Thực hành Lab 28: Workshop khởi đầu Immersion Day của Sagemaker**<br>+ Chuẩn bị<br>* Tạo SageMaker Studio<br>* Tải GitHub repo<br>+ Feature Engineering<br>* Chuẩn bị Dataset<br>* Cài đặt Data Wrangler<br>* Phân tích Dataset<br>* Phân tích tương quan<br>* Chuyển đổi dữ liệu<br>* Feature Store<br>* Export Data tới S3<br>+ Train/Tune/Deploy XGBoost<br>* Train & Tune model<br>* Deploy model<br>* Đánh giá hiệu suất model<br>* Tune model tự động<br>+ Dọn dẹp tài nguyên | 25/03/2026 | 25/03/2026 | [Lab 28 Prepare](https://000200.awsstudygroup.com/vi/1-prepare/)<br>[Feature Engineering](https://000200.awsstudygroup.com/vi/2-feature-engineering/)<br>[Train Deploy](https://000200.awsstudygroup.com/vi/3-train-tune-deploy/) |
| **5** | **- Họp team project: Phát triển backend - RAG system (được kết hợp từ hybrid search engine và LLM):**<br>- Chạy, kiểm thử hệ thống RAG với data đã thu thập<br>- Hoàn thiện hệ thống RAG | 26/03/2026 | 26/03/2026 | [Hybrid for RAG](https://careers.edicomgroup.com/techblog/llm-rag-improving-the-retrieval-phase-with-hybrid-search/)<br>[Medium RAG](https://medium.com/data-science/how-to-use-hybrid-search-for-better-llm-rag-retrieval-032f66810ebe)<br>[AWS RAG](https://aws.amazon.com/vi/what-is/retrieval-augmented-generation/)<br>[RAG Paper 2020](https://arxiv.org/pdf/2005.11401) |
| **6** | **- Thực hành Lab 29: AWS Toolkit for VS Code: Amazon Q & CodeWhisperer**<br>+ Giới thiệu<br>+ AWS Toolkit Cho Visual Studio Code<br>+ Kết nối tài khoản AWS<br>+ Thay đổi AWS Region<br>+ Xác thực<br>* IAM Identity Center<br>* AWS IAM credentials<br>* Tạo AWS Builder ID<br>+ Tương tác với các dịch vụ<br>* AWS Explorer<br>* Amazon Q<br>* Amazon CodeWhisperer | 27/03/2026 | 27/03/2026 | [Lab 29 Intro](https://000087.awsstudygroup.com/vi/1-introduce/)<br>[Install Toolkit](https://000087.awsstudygroup.com/vi/2-install/)<br>[Authentication](https://000087.awsstudygroup.com/vi/5-authentication-and-access-for-the-aws-toolkit-for-visual-studio-code/)<br>[Amazon Q](https://000087.awsstudygroup.com/vi/6-working-with-aws-services/) |


### THÀNH TỰU ĐẠT ĐƯỢC TRONG WEEK 11:
1. Nâng cấp thành công Hybrid Search Engine thành hệ thống RAG, cho phép người dùng tương tác bằng ngôn ngữ tự nhiên (Chat) thay vì chỉ gõ từ khóa.
2. Triển khai hoàn chỉnh ứng dụng Serverless đa chức năng (bao gồm xử lý ảnh thời gian thực) sử dụng AWS SAM (Serverless Application Model).
3. Hoàn thành pipeline Machine Learning trên SageMaker: Từ khâu làm sạch dữ liệu (Data Wrangler) đến huấn luyện và triển khai model XGBoost.
4. Cấu hình thành công môi trường lập trình tích hợp AI (Amazon Q, CodeWhisperer) trên VS Code, giúp tăng tốc độ viết code và debug.
5. Vận hành thử nghiệm hệ thống RAG với dữ liệu thực tế, đảm bảo tính chính xác và ngữ cảnh của câu trả lời.