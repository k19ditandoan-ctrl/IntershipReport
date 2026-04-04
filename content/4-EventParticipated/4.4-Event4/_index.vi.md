---
title: "Sự Kiện 4"
date: 2026-04-04
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# Báo Cáo Tóm Tắt: "Sự kiện Cloud Mastery: Infrastructure as Code"

### Tổng Quan Sự Kiện

- **Tên Sự Kiện:** Cloud Mastery - Infrastructure as Code (IaC)
- **Ngày:** 04 tháng 04, 2026
- **Vai Trò:** Người tham dự
- **Chủ Đề:** Quản lý hạ tầng bằng code và so sánh các công cụ (CloudFormation, CDK, Terraform)

Sự kiện đi sâu vào phương pháp Infrastructure as Code (IaC), cách nó thay đổi cách chúng ta triển khai và quản lý hạ tầng đám mây, cùng với thực hành và so sánh các công cụ phổ biến nhất hiện nay trên hệ sinh thái AWS và đa nền tảng.

### Nội Dung Chi Tiết

#### 1. Tổng quan về Infrastructure as Code (IaC)
**Định nghĩa:**
IaC là phương pháp quản lý, cấu hình và triển khai hạ tầng công nghệ thông tin thông qua code thay vì thực hiện các thao tác thủ công (click chuột qua giao diện).

**Chức năng chính:**
- Tự động hóa quá trình tạo, cập nhật và xóa các resource trên cloud.
- Triển khai hạ tầng một cách có thể lặp lại (reproducible) ở các môi trường khác nhau.

**Vấn đề của cách truyền thống (ClickOps):**
- Thao tác chậm và tốn thời gian.
- Rất dễ xảy ra sai sót do con người (human error).
- Thiếu tính nhất quán giữa các môi trường (Dev, Test, Prod).
- Khó khăn trong việc phối hợp (collaboration) và audit lịch sử thay đổi.

**Lợi ích của IaC đem lại:**
- **Automation:** Tự động hoá hoàn toàn quy trình.
- **Reproducibility:** Dễ dàng nhân bản môi trường.
- **Scalability:** Mở rộng nhanh chóng.
- **Collaboration:** Cho phép team Ops làm việc như team Code (có review, version control).

#### 2. Các công cụ IaC phổ biến trên AWS
Hiện nay có 3 công cụ chính được sử dụng rộng rãi khi làm việc với AWS:
- **AWS CloudFormation**
- **AWS CDK (Cloud Development Kit)**
- **Terraform**

#### 3. AWS CloudFormation
**Khái niệm:** Là công cụ IaC native của AWS, sử dụng YAML hoặc JSON để viết template. Tài nguyên được quản lý theo nhóm gọi là **Stack**.

**Thành phần chính:**
- **Template:** Blueprint định nghĩa hạ tầng cần triển khai.
- **Stack:** Tập hợp các resource thực tế được sinh ra và deploy cùng nhau từ template.

**Cách hoạt động:**
- Viết / Định nghĩa ra template (local).
- Upload template lên S3 hoặc trực tiếp qua AWS.
- Cấu hình và Deploy stack.
- AWS engine tự động phân tích dependency và provision resource tương ứng.

**Configuration Drift:**
- Đây là hiện tượng xảy ra khi tài nguyên bị ai đó chỉnh sửa thủ công (qua Console/CLI) bên ngoài CloudFormation.
- **Drift Detection:** CloudFormation cung cấp tính năng phát hiện sự sai lệch này. Tuy nhiên hệ thống chỉ thông báo chứ không tự sửa, kỹ sư phải tự quyết định update lại template để khớp cấu hình mới hay revert cấu hình thủ công.

#### 4. AWS CDK (Cloud Development Kit)
**Khái niệm:** Là một framework IaC cho phép dùng ngôn ngữ lập trình thực sự (TypeScript, Python, Java, C#, Go) để định nghĩa resource thay vì dùng JSON/YAML khô khan.

**Kiến trúc:** App → Stack → Construct
Cấu trúc thành **3 cấp độ Construct:**
- **L1:** Mapping trực tiếp 1-1 với resource của CloudFormation (low-level).
- **L2:** Abstraction cao hơn, cung cấp sẵn các default best-practices.
- **L3 (Patterns):** Một hệ sinh thái hoàn chỉnh liên kết nhiều tài nguyên (ví dụ: ALB kết hợp Fargate).

**Ưu điểm:**
- Đặc biệt thân thiện với Developer.
- Cho phép áp dụng logic lập trình (if/else, loop) và tính kế thừa (OOP) để tái sử dụng code.
- Tích hợp mượt mà với workflow của các IDE hiện đại.

**Các CLI quan trọng cần nhớ:** 
`cdk init`, `cdk bootstrap`, `cdk synth`, `cdk deploy`, `cdk destroy`, `cdk diff`, `cdk drift`.

#### 5. Terraform
**Khái niệm:** Công cụ IaC mã nguồn mở do HashiCorp phát triển, dùng ngôn ngữ HCL (HashiCorp Configuration Language). Điểm mạnh nhất là hỗ trợ **Multi-cloud** (AWS, Azure, GCP, on-premise).

**Điểm mạnh:**
- Quản lý trạng thái thông qua file **State** (`terraform.tfstate`), cho phép theo dõi chính xác sự thay đổi.
- Cú pháp khai báo đơn giản, rất rành mạch.
- Hỗ trợ hầu hết API của các nhà cung cấp cloud.

**Workflow chuẩn của Terraform:**
`terraform init` → `terraform validate` → `terraform plan` → `terraform apply` → `terraform destroy`.

**Cấu trúc project tiêu chuẩn:**
- `main.tf`: Chứa tài nguyên chính.
- `variables.tf`: Định nghĩa tham số đầu vào.
- `outputs.tf`: Kết quả sau khi provision.
- `providers.tf`: Cấu hình cloud provider.

#### 6. So sánh nhanh & Nguyên tắc chọn công cụ

| CÔNG CỤ | ĐIỂM MẠNH CHÍNH | USE-CASE KHUYẾN NGHỊ |
|---|---|---|
| **CloudFormation** | Native AWS, miễn phí, ổn định | Dự án 100% AWS thuần túy, team thiên hướng system |
| **AWS CDK** | Dùng ngôn ngữ lập trình, abstraction mạnh | Dev tự lo hạ tầng (DevOps), dự án cần logic phức tạp |
| **Terraform** | Hỗ trợ Multi-cloud, hệ sinh thái Provider siêu lớn | Hệ thống lớn, cross-cloud, chuẩn công nghiệp chung |

**Nguyên tắc chọn IaC tool:**
1. Doanh nghiệp dùng 1 cloud (AWS) hay multi-cloud? (Nếu multi-cloud → ưu tiên Terraform).
2. Team thiên về Dev (thích code như TypeScript) hay Ops (thích configuration như HCL/YAML)?
3. Ecosystem có sẵn của hệ thống CI/CD hỗ trợ tool nào tốt hơn?

### Insight Quan Trọng Nhận Được 
*(Ứng dụng cho thiết kế hệ thống thực tế)*

- **Bản chất của IaC:** Không chỉ đơn thuần là việc tự động hóa, mà cốt lõi là mang lại **Version Control cho Infrastructure**, cho phép review hạ tầng giống như review code.
- **Rủi ro Configuration Drift:** Đây là một rủi ro tiềm ẩn rất đáng sợ ở môi trường Production. Cần có quy trình CI/CD kết hợp Drift Tracking tooling chặt chẽ để cấm các thao tác ClickOps.
- **Thực tế về CDK và Amplify:** CDK thực chất chỉ là một lớp abstraction (abstraction layer), sau khi "synth" (biên dịch), nó vẫn sinh ra CloudFormation template. Dịch vụ AWS Amplify ở nền tảng bên dưới cũng hoạt động dựa trên cơ chế CloudFormation.
- **Terraform:** Hiện nay vẫn đang được coi là **tiêu chuẩn chung của ngành công nghiệp** (industry standard) do khả năng làm việc liên đám mây tuyệt vời của nó.


### Ảnh Sự Kiện

![AWS Community Day Vietnam](/images/4-Event/event4.jpg)
![AWS Community Day Vietnam](/images/4-Event/event4.1.jpg)

