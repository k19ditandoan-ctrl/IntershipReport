---
title: "Blog 3"
date: 2025-09-09
weight: 3
chapter: false
pre: " <b> 3.3. </b> "

---

---
title: "Blog 3"
date: 2025-09-09
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Cách UNiDAYS mở rộng Region trên AWS trong 3 tuần

bởi Sanhawat Taongern và Andrew Carter vào | ngày 08 tháng 4 2025 | trong [Amazon CloudFront](https://aws.amazon.com/blogs/architecture/category/networking-content-delivery/amazon-cloudfront/), [Amazon DynamoDB](https://aws.amazon.com/blogs/architecture/category/database/amazon-dynamodb/), [Amazon Elastic Container Registry](https://aws.amazon.com/blogs/architecture/category/compute/amazon-elastic-container-registry/), [Amazon Elastic Container Service](https://aws.amazon.com/blogs/architecture/category/compute/amazon-elastic-container-service/), [Amazon EventBridge](https://aws.amazon.com/blogs/architecture/category/application-integration/amazon-eventbridge/), [Amazon Route 53](https://aws.amazon.com/blogs/architecture/category/networking-content-delivery/amazon-route-53/), [AWS CloudFormation](https://aws.amazon.com/blogs/architecture/category/management-tools/aws-cloudformation/), [AWS WAF](https://aws.amazon.com/blogs/architecture/category/security-identity-compliance/aws-waf/), [Customer Solutions](https://aws.amazon.com/blogs/architecture/category/post-types/customer-solutions/)

[UNiDAYS](https://www.myunidays.com/) là một nền tảng kỹ thuật số nhanh, miễn phí, cung cấp các ưu đãi và lợi ích độc quyền cho sinh viên đã được xác minh với hơn 29 triệu thành viên trên toàn cầu. Với cơ sở người dùng tăng nhanh và số lượng quan hệ đối tác toàn cầu ngày càng nhiều, UNiDAYS nhận thấy sự cần thiết phải nâng cao hiệu suất nền tảng để mang lại trải nghiệm liền mạch cho người dùng ở các vùng địa lý xa so với trụ sở hoạt động ban đầu của mình. 

Trong bài viết này, chúng tôi chia sẻ cách UNiDAYS đã đạt được việc mở rộng Region AWS chỉ trong 3 tuần bằng cách sử dụng các dịch vụ AWS.

### **Thách thức kinh doanh**

Đáp lại các cơ hội tăng trưởng, UNiDAYS đối mặt với một yêu cầu cấp bách về mặt kinh doanh: cung cấp phản hồi độ trễ thấp và đảm bảo tính khả dụng cao cho người dùng ở nhiều vùng địa lý khác nhau. Đồng thời, nền tảng cần đảm bảo tính nhất quán dữ liệu toàn cầu trong khi tuân thủ hạn chót chặt chẽ — tất cả chỉ trong vài tuần. Tuy nhiên, ứng dụng hiện tại — mặc dù được xây dựng trên [Amazon Web Services](https://aws.amazon.com/) (AWS) — không được tối ưu cho việc triển khai active-active multi-Region.

Thách thức còn phức tạp hơn bởi việc mở rộng chức năng từ hệ thống kế thừa này, vốn sử dụng mạng toàn cầu của AWS để cải thiện trải nghiệm người dùng nhưng không đáp ứng đầy đủ các yêu cầu kinh doanh mới. Việc thiết kế lại toàn bộ nền tảng để hỗ trợ triển khai multi-Region trong khung thời gian này là điều không khả thi.

### **Tổng quan giải pháp**

UNiDAYS đã chọn tạo các dịch vụ bổ sung phù hợp với các yêu cầu mới này, sử dụng các dịch vụ AWS cho kiến trúc multi-Region, active-active. Các dịch vụ chủ chốt được sử dụng bao gồm:

- [Amazon CloudFront](https://aws.amazon.com/cloudfront/) và [Amazon Route 53](https://aws.amazon.com/route53/) – Để phân phối toàn cầu và phản hồi độ trễ thấp nhất


- [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) – Để cung cấp dữ liệu nhất quán, khả dụng cao giữa các Region


- [Amazon Elastic Container Service](https://aws.amazon.com/ecs/) (Amazon ECS) – Cho các tài nguyên đóng gói container có khả năng mở rộng và triển khai


- [Amazon EventBridge](https://aws.amazon.com/eventbridge/) – Để tích hợp bất đồng bộ với hệ thống hiện tại thông qua các mẫu event-driven


Cách tiếp cận này cho phép UNiDAYS đạt được các mục tiêu về độ trễ, khả dụng và tính nhất quán trong khi tích hợp liền mạch với hạ tầng hiện có. Sơ đồ dưới đây là kiến trúc của giải pháp.

![Enter image alt description](/images/3-Blog/blog3_figure1.png)

#### **Phân phối toàn cầu và khả năng phục hồi**

Để đưa lại độ trễ thấp nhất và khả năng chịu lỗi nhiều Region, CloudFront được sử dụng với [ ](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-latency.html)[latency-based routing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-latency.html) cấu hình trong Route 53. Việc định tuyến này hướng các yêu cầu đến các Application Load Balancers vùng (Regional) có độ trễ thấp nhất, tự động cung cấp khả năng phục hồi trong trường hợp có sự cố vùng Region. Bảo mật là một yếu tố quan trọng. Tích hợp [AWS WAF](https://aws.amazon.com/waf/) với CloudFront cung cấp bảo vệ ứng dụng ở lớp biên. Các biện pháp bảo mật bổ sung bao gồm:

- [HTTP header tùy chỉnh](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/header-modification.html) trên các yêu cầu origin, được thực thi bằng quy tắc listener của Application Load Balancer 


- [Danh sách tiền tố](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-aws-managed-prefix-lists.html) để hạn chế quyền truy cập vào Application Load Balancers, đảm bảo lưu lượng xuất phát từ các phân phối CloudFront dự định 


#### **Triển khai nhanh vùng Region**

Cơ sở hạ tầng lõi được triển khai thông qua Terraform, và các ứng dụng được triển khai sử dụng công cụ tùy chỉnh mà đóng gói [AWS CloudFormation](http://aws.amazon.com/cloudformation). Cách tiếp cận lai này cho phép triển khai nhanh chóng bằng cách sử dụng các mẫu sẵn có mà không làm gián đoạn các quy trình công việc đã thiết lập. Các tài nguyên được tổ chức thành các tầng: nền tảng (platform), toàn cầu (global), và từng Region (Regional). Các tài nguyên nền tảng và toàn cầu được triển khai một lần, và các tài nguyên Region được triển khai cho mỗi Region được kích hoạt, giúp đơn giản hóa các nỗ lực mở rộng.

Một thách thức kỹ thuật liên quan là [CloudFormation exports](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-stack-exports.html), vốn theo thiết kế là theo vùng Region. Để giải quyết điều này, họ đã triển khai một macro CloudFormation tùy chỉnh để cho phép truy cập các giá trị export qua các Region, đảm bảo tính nhất quán giữa các triển khai. 

Amazon ECS cho phép triển khai ứng dụng theo lộ trình (progressive deployments) trong từng Region, cho phép các nhóm tập trung vào mở rộng các ứng dụng hơn là quản lý cơ sở hạ tầng. Để tiết kiệm chi phí, họ sử dụng Spot Instances. Trong quá trình thử nghiệm, độ trễ khi khởi động container được quan sát do việc tải hình ảnh container qua Region từ  [Amazon Elastic Container Registry](https://aws.amazon.com/ecr/) (ECR). Vấn đề này được giải quyết bằng cách [kích hoạt private image replication](https://docs.aws.amazon.com/AmazonECR/latest/userguide/replication.html) trong Amazon ECR sao cho hình ảnh container có sẵn cục bộ ở mỗi Region. Giải pháp này giảm đáng kể thời gian khởi động, cải thiện khả năng phản hồi ứng dụng trong quá trình triển khai và sự kiện mở rộng.

#### **Tính nhất quán dữ liệu và hiệu suất**

[DynamoDB global tables](https://aws.amazon.com/dynamodb/global-tables/) đóng vai trò quan trọng trong việc cung cấp tính nhất quán dữ liệu theo thời gian (eventual consistency) và sao chép giữa các Region. Với DynamoDB xử lý các khía cạnh này, UNiDAYS có thể tập trung vào logic ứng dụng.

Kết quả là độ trễ tại các vị trí chính giảm đáng kể. Ví dụ, độ trễ trải nghiệm của khách hàng tại một Region giảm từ khoảng 200 mili-giây xuống còn 50 mili-giây sau khi triển khai.

![Enter image alt description](/images/3-Blog/blog3_figure2.png)

### **Những rào cản kỹ thuật chính**

Chúng tôi đã giải quyết các trở ngại kỹ thuật sau trong quá trình phát triển giải pháp:

- **CloudFormation exports qua các Region** — vì exports vốn thiết kế theo Region. Họ tạo macro CloudFormation tùy chỉnh để đọc export qua các Region. 


- **Độ trễ khi khởi động container **— do việc tải hình ảnh container qua các Region; được khắc phục bằng việc cấu hình ECR private image replication để hình ảnh có sẵn ở mọi Region, giảm thời gian triển khai. 


- **Đảm bảo bảo mật** — bằng cách sử dụng CloudFront, AWS WAF, và các tính năng bảo mật của Application Load Balancer, đảm bảo lưu lượng và dữ liệu luôn được bảo vệ. 


### **Tại sao chọn AWS?**

UNiDAYS chọn AWS vì cơ sở hạ tầng toàn cầu phong phú và các dịch vụ mạnh mẽ, cho phép nền tảng:

- Mở rộng hoạt động compute sang các Region gần hơn với người dùng của mình một cách liền mạch

- Tận dụng bộ dịch vụ đầy đủ cho phân phối nội dung đáng tin cậy, bảo mật và độ trễ thấp

- Hoàn thành các hạn giao tight deadline mà không làm ảnh hưởng tới hiệu suất hoặc bảo mật

- Duy trì tính linh hoạt khi cần, với khả năng sử dụng nhiều dịch vụ được quản lý, cho phép tập trung vào ứng dụng của mình

### **Kết luận**

Bằng cách áp dụng kiến trúc multi-Region, active-active trên AWS, UNiDAYS đã đạt được các mục tiêu kinh doanh chỉ trong 3 tuần, mở rộng nhanh sang các Region mới trong khi thúc đẩy độ chịu lỗi của nền tảng. Giải pháp đã cải thiện độ trễ khoảng 75% ở các Region mới (từ 200 mili-giây xuống 50 mili-giây), cung cấp khả năng sẵn sàng dữ liệu vùng Regional thông qua bảng toàn cầu của DynamoDB, và duy trì thời gian hoạt động dịch vụ 100% trong các thử nghiệm độ chịu lỗi ngay cả khi mất kết nối Region. Thêm vào đó, tốc độ triển khai tính năng tăng hơn 40%, cho phép phát hành tính năng nhanh hơn và cải thiện tính linh hoạt. Kiến trúc này không chỉ mang lại một nền tảng có khả năng mở rộng và chịu lỗi cho hoạt động hiện tại mà còn xây dựng nền móng mạnh mẽ cho việc mở rộng toàn cầu trong tương lai.

### **Tìm hiểu thêm**

Liệu tổ chức của bạn có muốn mở rộng sang các Region mới trong khi vẫn duy trì hiệu suất và độ tin cậy?

- Liên hệ các chuyên gia AWS để khám phá các giải pháp tùy chỉnh cho chiến lược multi-Region của bạn.

- Sử dụng AWS Global Infrastructure để tối ưu hóa việc mở rộng.

- Chia sẻ các thách thức và thành công của bạn trong phần bình luận — chúng tôi rất muốn nghe những hiểu biết của bạn!

#### **Về các tác giả**

![Enter image alt description](/images/3-Blog/blog3_figure3.jpeg)
**Sanhawat Taongern**

Sanhawat Taongern là Kiến trúc sư Giải pháp (Solutions Architect) tại AWS, làm việc với các khách hàng doanh nghiệp trong lĩnh vực Truyền thông và Quảng cáo. Anh đã hợp tác với nhiều khách hàng thuộc các phân khúc và khu vực khác nhau, giúp họ đổi mới và chuyển đổi doanh nghiệp bằng cách sử dụng các dịch vụ của AWS. Anh chuyên về thiết kế và triển khai các giải pháp đám mây có khả năng mở rộng, giúp các doanh nghiệp đẩy nhanh hành trình chuyển đổi số của mình.


![Enter image alt description](/images/3-Blog/blog3_figure4.jpeg)
**Andrew Carter**

Andrew Carter là Kỹ sư Nền tảng cấp cao (Staff Platform Engineer) tại UNiDAYS. Với hơn 16 năm kinh nghiệm trong lĩnh vực kỹ thuật phần mềm và phát triển đám mây, anh đam mê xây dựng các nền tảng có khả năng mở rộng và đáng tin cậy, giúp các nhà phát triển đạt được kết quả tốt hơn trong khi rút ngắn thời gian phát triển. Tập trung vào trải nghiệm người dùng, Andrew là một người ủng hộ mạnh mẽ cho DevOps, thích chia sẻ kiến thức của mình và khám phá các công nghệ mới.
