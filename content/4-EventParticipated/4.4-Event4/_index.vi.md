---
title: "Sự Kiện 4"
date: 2025-09-09
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# Báo Cáo Tóm Tắt: "AIML & Generative AI trên AWS – AWS Cloud Mastery Series #1"

### Tổng Quan Sự Kiện

- **Tên Sự Kiện:** AIML & Generative AI trên AWS – AWS Cloud Mastery Series #1  
- **Ngày:** 15 tháng 11, 2025  
- **Vai Trò:** Người tham dự  
- **Hình Thức:** Phiên kỹ thuật tại chỗ  
- **Thời Lượng:** Phiên trọn ngày (8:30 AM – 11:00 AM+)
- **Địa Điểm:** Tầng 26, Tòa nhà Bitexco Financial Tower, Quận 1, Thành phố Hồ Chí Minh, Việt Nam

Phiên kỹ thuật toàn diện này là một phần của AWS Cloud Mastery Series, tập trung cụ thể vào trí tuệ nhân tạo, machine learning, và khả năng generative AI trên AWS. Sự kiện cung cấp cả nền tảng lý thuyết và insights thực tế về xây dựng giải pháp AI/ML sử dụng các dịch vụ AWS.

### Chương Trình Phiên

#### Phiên 1: Tổng Quan AI/ML (8:30 – 9:00 AM)
**Diễn Giả:** Lam Tuan Kiet

##### Nền Tảng Machine Learning
- **Supervised Learning**: Hiểu các tác vụ nơi models học từ dữ liệu có nhãn
  - Classification: Phân loại dữ liệu thành các lớp
  - Regression: Dự đoán các giá trị liên tục
  - Các algorithms và use cases phổ biến
- **Deep Learning**: Neural networks và ứng dụng của chúng
  - Multi-layer perceptrons
  - Convolutional Neural Networks (CNNs) cho xử lý hình ảnh
  - Recurrent Neural Networks (RNNs) cho dữ liệu chuỗi
  - Kiến trúc Transformers

##### Foundation Models và Generative AI
- **Foundation Models**: Các models được pre-train lớn phục vụ như cơ sở cho các tác vụ khác nhau
  - Điều gì làm cho một model trở thành "foundation model"
  - Lợi ích của việc sử dụng models được pre-train
  - Khái niệm transfer learning
- **Generative Models**: Models tạo nội dung mới
  - Hiểu unsupervised learning trong ngữ cảnh generative AI
  - Cách generative models khác với discriminative models
  - Ứng dụng: tạo văn bản, tạo hình ảnh, tạo mã

##### Prompt Engineering
- **Prompt là gì?**: Hiểu prompts như hướng dẫn cho AI models
- **Prompt Tốt vs Prompt Tệ**: 
  - Đặc điểm của prompts hiệu quả (rõ ràng, cụ thể, có ngữ cảnh)
  - Các lỗi phổ biến trong thiết kế prompt
  - Ví dụ về prompts được xây dựng kém và cách cải thiện chúng
- **Zero-shot Prompting**: Nhận kết quả mà không cần examples
  - Khi nào zero-shot hoạt động tốt
  - Giới hạn và cân nhắc
- **Few-shot Prompting**: Cung cấp examples để hướng dẫn hành vi model
  - Cách few-shot learning cải thiện kết quả
  - Best practices cho việc chọn examples
  - Cân bằng chất lượng và số lượng example

##### Chain of Thought Reasoning
- **Chain of Thought là gì?**: Chia nhỏ các vấn đề phức tạp thành các bước
- **Lợi Ích**: Cải thiện khả năng lý luận của language models
- **Triển Khai**: Cách cấu trúc prompts để khuyến khích suy nghĩ từng bước
- **Ứng Dụng**: Giải quyết vấn đề, lý luận toán học, phân tích logic

##### Retrieval-Augmented Generation (RAG)
- **Tổng Quan RAG**: Kết hợp retrieval với generation để có độ chính xác tốt hơn
- **RAG Flow**: 
  - **Retrieval**: Tìm thông tin liên quan từ knowledge bases
  - **Augmentation**: Tăng cường prompts với ngữ cảnh được retrieve
  - **Generation**: Tạo responses dựa trên prompts được augment
- **Embeddings**: 
  - Embeddings là gì và cách chúng biểu diễn ý nghĩa ngữ nghĩa
  - Vector embeddings vs tìm kiếm từ khóa truyền thống
  - Cách embeddings cho phép semantic search
- **Amazon Titan Embeddings**: 
  - Khả năng embedding model của AWS
  - Use cases cho Titan embeddings
  - Tích hợp với các dịch vụ AWS khác
- **RAG Workflows**:
  - **Data Ingestion Workflow**: Chuẩn bị và indexing documents cho retrieval
    - Xử lý và chunking documents
    - Tạo embeddings
    - Lưu trữ trong vector databases
  - **Text Generation Workflow**: Sử dụng RAG cho trả lời truy vấn
    - Xử lý và embedding truy vấn
    - Similarity search
    - Context augmentation
    - Response generation

#### Phiên 2: Dịch Vụ AI/ML AWS (9:00 – 10:00 AM)
**Diễn Giả:** Dinh Le Hoang Anh

Phiên này cung cấp tổng quan toàn diện về các dịch vụ AI/ML được quản lý của AWS ngoài Amazon Bedrock, bao gồm các dịch vụ chuyên biệt cho các use case khác nhau.

##### Dịch Vụ Computer Vision

**Amazon Rekognition**
- **Xử Lý Hình Ảnh và Video**: Phân tích nội dung trực quan ở quy mô lớn
- **Nhận Dạng Đối Tượng**: Xác định và gắn nhãn objects trong hình ảnh
- **Phát Hiện và Phân Tích Khuôn Mặt**: 
  - Phát hiện khuôn mặt trong hình ảnh và video
  - So sánh và xác minh khuôn mặt
  - Phân tích thuộc tính khuôn mặt
- **Kiểm Duyệt Nội Dung**: 
  - Phát hiện nội dung không phù hợp hoặc không an toàn
  - Custom moderation models
- **Nhận Dạng Người Nổi Tiếng**: Xác định các nhân vật nổi tiếng
- **Custom Labeling**: 
  - Training custom models cho các tác vụ nhận dạng cụ thể
  - Use cases cho phân loại hình ảnh theo domain
  - Workflow để tạo custom models

##### Dịch Vụ Xử Lý Ngôn Ngữ Tự Nhiên

**Amazon Translate**
- **Dịch Nhận Biết Ngữ Cảnh**: Hiểu ngữ cảnh để dịch tốt hơn
- **Dịch Real-time**: Dịch độ trễ thấp cho ứng dụng
- **Nhận Dạng Ngôn Ngữ**: Tự động phát hiện ngôn ngữ nguồn
- **Thuật Ngữ Tùy Chỉnh**: Sử dụng từ điển dịch theo domain
- **Dịch Hàng Loạt**: Xử lý khối lượng văn bản lớn

**Amazon Textract**
- **Nhận Dạng Ký Tự Quang Học (OCR)**: Trích xuất văn bản từ hình ảnh và documents
- **Bảo Toàn Bố Cục**: Duy trì cấu trúc và định dạng document
- **Trích Xuất Form và Bảng**: Xác định và trích xuất dữ liệu có cấu trúc
- **Nhận Dạng Chữ Viết Tay**: Xử lý văn bản viết tay
- **Phân Tích Document**: Hiểu loại document và trích xuất thông tin quan trọng

**Amazon Transcribe**
- **Chuyển Đổi Giọng Nói Thành Văn Bản**: Chuyển đổi audio thành text
- **Nhận Dạng Người Nói**: Phân biệt giữa các người nói khác nhau
- **Lọc Nội Dung**: Lọc nội dung không phù hợp trong transcriptions
- **Từ Vựng Tùy Chỉnh**: Cải thiện độ chính xác với các thuật ngữ theo domain
- **Transcription Real-time**: Khả năng transcription trực tiếp
- **Hỗ Trợ Đa Ngôn Ngữ**: Transcription trong nhiều ngôn ngữ

**Amazon Polly**
- **Text-to-Speech**: Chuyển đổi văn bản thành giọng nói tự nhiên
- **Loại Giọng**: Nhiều giọng và ngôn ngữ có sẵn
- **Tổng Hợp Real-time**: Tạo giọng nói độ trễ thấp
- **Caching và Replay**: Tối ưu cho nội dung lặp lại
- **Hỗ Trợ SSML**: Markup tổng hợp giọng nói nâng cao

**Amazon Comprehend**
- **Trích Xuất Insights**: Hiểu sentiment, entities, và key phrases
- **Trích Xuất Mối Quan Hệ**: Xác định mối quan hệ giữa các entities
- **Topic Modeling**: Khám phá topics trong collections documents
- **Nhận Dạng Ngôn Ngữ**: Xác định ngôn ngữ của văn bản
- **Phân Loại Tùy Chỉnh**: Training custom text classifiers

##### Dịch Vụ Tìm Kiếm và Khám Phá

**Amazon Kendra**
- **Tìm Kiếm Ngữ Nghĩa**: Hiểu ý nghĩa, không chỉ từ khóa
- **Tìm Kiếm Thông Minh**: Khả năng tìm kiếm hỗ trợ bởi NLP
- **Hỗ Trợ RAG**: Tích hợp với retrieval-augmented generation
- **Tìm Kiếm Doanh Nghiệp**: Tìm kiếm trên nhiều nguồn dữ liệu
- **Nguồn Dữ Liệu Tùy Chỉnh**: Kết nối với các repositories nội dung khác nhau

##### Dịch Vụ Đề Xuất

**Amazon Personalize**
- **Đề Xuất Được Tùy Chỉnh**: Tạo trải nghiệm người dùng cá nhân hóa
- **Đề Xuất Real-time**: Tạo đề xuất độ trễ thấp
- **Đề Xuất Hàng Loạt**: Xử lý đề xuất cho cơ sở người dùng lớn
- **Models Tùy Chỉnh**: Training models trên dữ liệu của bạn
- **A/B Testing**: Testing các chiến lược đề xuất khác nhau

##### Frameworks Chuyên Biệt

**Pipecat**
- **Pipeline Framework**: Xây dựng voice và multimodal AI agents
- **Khả Năng Real-time**: Tối ưu cho tương tác real-time
- **Use Cases**: Voice assistants, ứng dụng tương tác
- **Tích Hợp**: Làm việc với dịch vụ AWS và công cụ AI khác

**Amazon Lookout Family**
- **Lưu Ý**: Các dịch vụ này đã được tích hợp vào các dịch vụ AWS khác
- **Ngữ Cảnh Lịch Sử**: Hiểu những gì Lookout services cung cấp
- **Đường Di Chuyển**: Cách chức năng chuyển sang các dịch vụ khác

#### Phiên 3: Amazon Bedrock AgentCore (10:00 – 11:00 AM)
**Diễn Giả:** Danh Hoang Hieu Nghi

Phiên này tập trung vào xây dựng AI agents sử dụng Amazon Bedrock AgentCore, bao gồm cả khái niệm và triển khai thực tế.

##### Tổng Quan Agent Frameworks
- **LangGraph**: Xây dựng ứng dụng stateful, multi-actor với LLMs
- **LangChain**: Framework để phát triển ứng dụng hỗ trợ bởi language models
- **LlamaIndex**: Data framework cho ứng dụng LLM
- **So Sánh**: Hiểu khi nào sử dụng mỗi framework
- **Tích Hợp**: Cách các frameworks này hoạt động với dịch vụ AWS

##### Quy Trình Tạo Agent
- **Giai Đoạn Lập Kế Hoạch**: Định nghĩa mục tiêu và khả năng agent
- **Giai Đoạn Thiết Kế**: Kiến trúc workflows và decision trees của agent
- **Giai Đoạn Phát Triển**: Triển khai logic và tích hợp agent
- **Giai Đoạn Testing**: Xác thực hành vi agent và edge cases
- **Giai Đoạn Triển Khai**: Đưa agents vào production

##### Thách Thức Production
- **Khả Năng Mở Rộng**: Xử lý tải tăng và người dùng đồng thời
- **Độ Tin Cậy**: Đảm bảo hiệu suất nhất quán và xử lý lỗi
- **Giám Sát**: Theo dõi hiệu suất agent và tương tác người dùng
- **Quản Lý Chi Phí**: Tối ưu chi phí trong khi duy trì chất lượng
- **Bảo Mật**: Bảo vệ dữ liệu nhạy cảm và ngăn chặn lạm dụng

##### Từ Khóa Amazon Bedrock AgentCore

**Runtime**
- **Môi Trường Thực Thi**: Nơi agents chạy và thực thi
- **Tối Ưu Hiệu Suất**: Đảm bảo thời gian phản hồi nhanh
- **Quản Lý Tài Nguyên**: Phân bổ và quản lý compute resources

**Memory**
- **Lịch Sử Cuộc Trò Chuyện**: Duy trì ngữ cảnh qua các tương tác
- **Bộ Nhớ Dài Hạn**: Lưu trữ thông tin cho các phiên tương lai
- **Quản Lý Bộ Nhớ**: Chiến lược lưu trữ và truy xuất hiệu quả

**Identity**
- **Nhận Dạng Người Dùng**: Xác định và xác thực người dùng
- **Quản Lý Phiên**: Quản lý sessions và state của người dùng
- **Hỗ Trợ Đa Người Dùng**: Xử lý nhiều người dùng đồng thời

**Gateway**
- **API Gateway**: Expose agents qua APIs
- **Điểm Tích Hợp**: Kết nối agents với các hệ thống khác
- **Định Tuyến Yêu Cầu**: Hướng requests đến agents phù hợp

**Code Interpreter**
- **Thực Thi Mã**: Chạy mã trong workflows của agent
- **Sandboxing**: Môi trường thực thi an toàn
- **Use Cases**: Phân tích dữ liệu, tính toán, tạo nội dung động

**Browser Tool**
- **Tương Tác Web**: Cho phép agents tương tác với nội dung web
- **Truy Xuất Thông Tin**: Lấy và xử lý dữ liệu web
- **Tự Động Hóa**: Tự động hóa các tác vụ dựa trên web

**Observability**
- **Giám Sát**: Theo dõi hiệu suất và hành vi agent
- **Ghi Log**: Ghi lại tương tác và quyết định của agent
- **Phân Tích**: Hiểu patterns sử dụng agent
- **Debugging**: Công cụ để khắc phục sự cố agent

##### Dịch Vụ AgentCore Cho Quy Mô
- **Hệ Thống Đa Agent**: Phối hợp nhiều agents
- **Cân Bằng Tải**: Phân phối tải trên các instances agent
- **Tự Động Mở Rộng**: Tự động điều chỉnh capacity
- **High Availability**: Đảm bảo agents luôn có sẵn
- **Tính Năng Doanh Nghiệp**: Bảo mật, tuân thủ, và quản trị

### Kiến Thức Kỹ Thuật Quan Trọng

#### Nền Tảng AI/ML
- Hiểu rõ sự khác biệt giữa ML truyền thống, deep learning, và generative AI
- Cách foundation models cho phép các loại ứng dụng mới
- Tầm quan trọng của prompt engineering trong việc có kết quả tốt từ generative models

#### Kiến Trúc RAG
- Hiểu biết hoàn chỉnh về RAG workflows từ data ingestion đến text generation
- Cách embeddings cho phép semantic search và cải thiện chất lượng retrieval
- Kiến thức thực tế về triển khai hệ thống RAG trên AWS

#### Hệ Sinh Thái Dịch Vụ AWS
- Tổng quan toàn diện về dịch vụ AI/ML AWS và khi nào sử dụng mỗi dịch vụ
- Hiểu rằng các dịch vụ khác nhau giải quyết các vấn đề khác nhau
- Cách các dịch vụ có thể được kết hợp cho các giải pháp phức tạp

#### Phát Triển Agent
- Hiểu độ phức tạp của việc xây dựng AI agents sẵn sàng cho production
- Các thành phần chính cần thiết cho hệ thống agent có khả năng mở rộng
- Best practices cho thiết kế và triển khai agent

### Bài Học Cá Nhân

#### Phát Triển Kỹ Thuật
- Tôi có được mô hình tinh thần có cấu trúc về GenAI stack hiện đại trên AWS
- Tôi hiểu cách các RAG pipelines được xây dựng end-to-end, từ chuẩn bị dữ liệu đến tạo response
- Tôi học được các managed services nào cần kết hợp khi thiết kế ứng dụng hỗ trợ AI

#### Insights Thực Tế
- Tầm quan trọng của prompt engineering không thể được đánh giá quá cao
- RAG là một pattern mạnh mẽ để xây dựng ứng dụng AI chính xác, nhận biết ngữ cảnh
- AWS cung cấp một bộ dịch vụ toàn diện bao phủ toàn bộ phổ AI/ML

#### Ứng Dụng Tương Lai
- Tôi rất vui mừng xây dựng ứng dụng dựa trên RAG sử dụng Amazon Bedrock và Titan embeddings
- Tôi muốn khám phá xây dựng agents sử dụng AgentCore cho các use case cụ thể
- Tôi thấy cơ hội kết hợp nhiều dịch vụ AI AWS cho các giải pháp toàn diện

#### Phát Triển Sự Nghiệp
- Sự kiện này củng cố sự quan tâm của tôi về AI/ML và generative AI
- Tôi hiểu phạm vi cơ hội trong không gian AI trên AWS
- Tôi có động lực tiếp tục học về kỹ thuật AI/ML nâng cao và dịch vụ AWS

### Trải Nghiệm Sự Kiện

Đây là một sự kiện cực kỳ thông tin cung cấp cả chiều rộng và chiều sâu. Sự tiến triển từ nền tảng đến dịch vụ cụ thể đến phát triển agent nâng cao đã cho tôi bức tranh hoàn chỉnh về AI/ML trên AWS.

Các diễn giả có kiến thức và cung cấp insights thực tế vượt ra ngoài chỉ mô tả tính năng. Các examples thực tế và use cases giúp tôi hiểu cách áp dụng các dịch vụ này trong thực tế.

Cấu trúc sự kiện cho phép nhịp độ tốt, với mỗi phiên xây dựng dựa trên các khái niệm trước đó. Sự kết hợp giữa lý thuyết và examples thực tế làm cho các chủ đề phức tạp trở nên dễ tiếp cận.

### Ảnh Sự Kiện

![AWS Community Day Vietnam](/images/4-Event/event4.jpg)
![AWS Community Day Vietnam](/images/4-Event/event4.1.jpg)

