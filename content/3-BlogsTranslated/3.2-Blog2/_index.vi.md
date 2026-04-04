---
title: "Blog 2"
date: 2025-09-09
weight: 2
chapter: false
pre: " <b> 3.2. </b> "

---

# Cách để có cái nhìn toàn tổ chức về các mua sắm trên AWS Marketplace

bởi Elhadj Barry, Atif Saeed và Juan Palazuelos | vào ngày 16 tháng 4 2025 | trong [Amazon Q](https://aws.amazon.com/blogs/awsmarketplace/category/amazon-q/), [AWS Cloud Financial Management](https://aws.amazon.com/blogs/awsmarketplace/category/aws-cloud-financial-management/), [AWS Marketplace](https://aws.amazon.com/blogs/awsmarketplace/category/software/aws-marketplace/), [Best Practices](https://aws.amazon.com/blogs/awsmarketplace/category/post-types/best-practices/), [Billing & Account Management](https://aws.amazon.com/blogs/awsmarketplace/category/aws-cloud-financial-management/billing-and-account-management/), [Business Intelligence](https://aws.amazon.com/blogs/awsmarketplace/category/business-intelligence/), [Enterprise governance and control](https://aws.amazon.com/blogs/awsmarketplace/category/management-and-governance/enterprise-governance-and-control/), [Management & Governance](https://aws.amazon.com/blogs/awsmarketplace/category/management-and-governance/), [Technical How-to](https://aws.amazon.com/blogs/awsmarketplace/category/post-types/technical-how-to/), [Thought Leadership](https://aws.amazon.com/blogs/awsmarketplace/category/post-types/thought-leadership/)

Việc quản lý tài sản phần mềm trên nhiều tài khoản Amazon Web Services (AWS) tạo ra những thách thức đối với các tổ chức lớn sử dụng [AWS Organizations](https://aws.amazon.com/organizations/). Các quản trị viên CNTT doanh nghiệp cần những cách tốt hơn để theo dõi và kiểm soát việc mua phần mềm từ các nhà cung cấp phần mềm độc lập (ISV) trên các tài khoản của họ.

Các tổ chức đối mặt với thách thức khi theo dõi thủ công tài sản phần mềm, đôi khi sử dụng bảng tính, điều này có thể dẫn đến sự thiếu minh bạch, quản lý chi phí kém, bỏ lỡ thời hạn gia hạn và mất cơ hội đàm phán. Bảng điều khiển [Procurement insights của ](https://docs.aws.amazon.com/organizations/latest/userguide/services-that-can-integrate-procurement-insights.html)[AWS Marketplace ](https://docs.aws.amazon.com/organizations/latest/userguide/services-that-can-integrate-procurement-insights.html)cung cấp một giải pháp tập trung, không mất phí để quản lý các giao dịch phần mềm trên các tài khoản.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Bài viết này giới thiệu bảng điều khiển Procurement insights của AWS Marketplace, cung cấp khả năng nhìn nhận cấp độ tổ chức đối với các giao dịch AWS Marketplace. Tìm hiểu cách công cụ này tăng cường minh bạch và kiểm soát, cho phép ra quyết định chiến lược cho việc mua sắm AWS Marketplace của bạn.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

### **Tổng quan giải pháp**

Bảng điều khiển Procurement insights của AWS Marketplace tập trung quyền nhìn nhận và quản lý các giao dịch AWS Marketplace trên toàn bộ doanh nghiệp. Bảng điều khiển hiển thị tất cả các hợp đồng phần mềm ISV, các khoản đã hóa đơn, việc gia hạn và ngày hết hạn ở một nơi.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Bạn truy cập bảng điều khiển thông qua [AWS Marketplace console](https://console.aws.amazon.com/marketplace/) hoặc nhúng nó vào công cụ của bạn qua API. Bảng điều khiển cung cấp các tính năng chính sau đây:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Minh bạch tập trung** – Xem tất cả các đăng ký và hợp đồng phần mềm AWS Marketplace ở một nơi, bao gồm ID tài khoản AWS đã mua, ID đề nghị (offer IDs), loại đề nghị, ID hợp đồng, và ngày bắt đầu & kết thúc hợp đồng.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Phân tích chi phí** – Xem dữ liệu chi tiêu AWS Marketplace, bao gồm các số liệu hóa đơn theo khoảng thời gian cụ thể, để hỗ trợ lập kế hoạch tài chính và quản lý ngân sách.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Kiểm toán và tuân thủ** – Theo dõi khi nào các điều khoản được chấp nhận, với mốc thời gian, chi tiết tài khoản và lịch sử hợp đồng. Việc theo dõi này tạo ra một dấu vết kiểm toán đáng tin cậy về chi tiêu AWS Marketplace của bạn để hỗ trợ việc duy trì tuân thủ các chính sách tổ chức và quy định ngành.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

### **Thiết lập bảng điều khiển**

Bảng điều khiển lấy dữ liệu từ các nguồn AWS để cung cấp cái nhìn toàn tổ chức. Trước khi sử dụng nó, bạn phải hoàn thành các bước sau. Lưu ý rằng chỉ người dùng tài khoản quản lý hoặc các quản trị viên được ủy quyền mới được truy cập bảng điều khiển này. Để biết thông tin về đăng ký và hủy đăng ký quản trị viên được ủy quyền, tham khảo phần [Using delegated administrators](https://docs.aws.amazon.com/marketplace/latest/buyerguide/management-delegates.html) trong tài liệu AWS.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

1. Bật tất cả các tính năng trong **AWS Organizations**. Để biết hướng dẫn, tham khảo tài liệu [Enabling all features for an organization with AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org_support-all-features.html).[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

2. Thêm các quyền sau vào chính sách IAM của bạn để **xem và sử dụng bảng điều khiển**:


- aws-marketplace:GetBuyerDashboard[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:DescribeOrganization[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- Thêm các quyền sau vào chính sách IAM của bạn để **bật bảng điều khiển**:


- iam:CreateServiceLinkedRole[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:EnableAWSServiceAccess[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:DisableAWSServiceAccess[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:DescribeOrganization[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:ListAWSServiceAccessForOrganization[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:ListDelegatedAdministrators (cần để quản lý các quản trị viên được ủy quyền)[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- organizations:DeregisterDelegatedAdministrator (cần để quản lý các quản trị viên được ủy quyền)[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- Bật cài đặt procurement insights của AWS Marketplace trong phần settings của AWS Marketplace console. Việc này tạo một [service-linked role](https://docs.aws.amazon.com/mSpecify%20where%20-%20in%20our%20case%20in%20the%20Organizations%20management%20account%0darketplace/latest/buyerguide/buyer-service-linked-role-procurement.html) và cho phép truy cập tin cậy (trusted access), cho phép AWS Marketplace truy cập thông tin cần thiết từ AWS Organizations. Để biết thêm chi tiết, tham khảo tài liệu [Activating the dashboard](https://docs.aws.amazon.com/marketplace/latest/buyerguide/enabling-procurement-insights.html#integrate-dashboard).[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Dữ liệu trong bảng điều khiển Procurement insights được lấy và xác minh từ nhiều nguồn dữ liệu. Do đó, các giao dịch AWS Marketplace mới có thể mất hơn 24 giờ để xuất hiện trong bảng điều khiển.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

### **Tính năng & hướng dẫn sử dụng**

Để truy cập bảng điều khiển, làm theo các bước sau:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

1. Đăng nhập vào [AWS Management Console](https://us-east-1.console.aws.amazon.com/marketplace/home#/procurement-insights) và mở AWS Marketplace console. Bạn cần quyền của chủ tài khoản quản lý hoặc quản trị viên được ủy quyền để truy cập bảng điều khiển.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

2. Trong tài khoản Quản lý hoặc tài khoản Quản trị viên Được ủy quyền đã đăng ký, chọn **Procurement insights**, như hình dưới đây. Nếu bạn chưa kích hoạt bảng điều khiển, tham khảo phần [Enabling the Procurement insights dashboard](https://docs.aws.amazon.com/marketplace/latest/buyerguide/enabling-procurement-insights.html).[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

3. Bảng điều khiển AWS Marketplace Procurement insights có hai phần chính:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

4. Tab **Cost analysis** – Xem dữ liệu chi tiêu trên các mua sắm AWS Marketplace của tổ chức bạn.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

5. Tab **Agreements** – Theo dõi các hợp đồng AWS Marketplace đang hoạt động và đã hết hạn trên toàn tổ chức. (Các hợp đồng đã hết hạn trong chế độ xem này chỉ được theo dõi từ thời điểm tính năng được kích hoạt)[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Bảng điều khiển AWS Marketplace Procurement Insights hiển thị các tab Phân tích chi phí và Thỏa thuận để theo dõi dữ liệu mua sắm, các thỏa thuận, và khả năng hiển thị chi tiêu.

![Enter image alt description](/images/3-Blog/blog2_figure1.png)

*Hình 1: Trang chính của AWS Marketplace Procurement Insights – Truy cập dữ liệu Phân tích chi phí và Thỏa thuận*

#### **Chế độ xem phân tích chi phí**

Khi bạn mở bảng điều khiển Procurement insights, chế độ xem mặc định là tab **Cost analysis**. Bạn có ba tùy chọn để lọc dữ liệu của mình:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Bảng điều khiển AWS Marketplace Procurement Insights hiển thị phân tích chi phí theo thỏa thuận, nhà bán hàng, sản phẩm và tài khoản, cùng với tổng chi phí trên các thỏa thuận.

![Enter image alt description](/images/3-Blog/blog2_figure2.png)

*Hình 2: Bảng điều khiển AWS Marketplace Procurement Insights – Phân tích chi phí theo Thỏa thuận, Nhà bán hàng, Sản phẩm và Tài khoản*

**Ngày hóa đơn** – Lọc các hợp đồng dựa trên khi chúng được hóa đơn.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Pay-as-you-go** – Xem các tùy chọn hàng năm và hợp đồng mà không bao gồm các hợp đồng pay-as-you-go.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Offer type** – Lọc theo loại đề nghị, chẳng hạn như đề nghị riêng tư hoặc công khai[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Phần **Total charges** hiển thị tổng số tiền tổ chức đã chi cho các hợp đồng AWS Marketplace. Dữ liệu này bao gồm chi tiêu từ các hợp đồng đang hoạt động và các hợp đồng trước đó.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Phần **Number of agreements** hiển thị số lượng hợp đồng AWS Marketplace của tổ chức bạn. Con số này bao gồm cả hợp đồng hiện tại và đã qua.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)Biểu đồ chuỗi thời gian **Total changes by agreement** hiển thị các khoản chi AWS Marketplace theo hợp đồng. Chế độ xem này hiển thị số lượng hợp đồng được hóa đơn trong khoảng thời gian được chỉ định, chứ không phải tổng số hợp đồng hiện có. Các “Free Trial Agreements” hoặc “Free Product Agreements” bị loại trừ, vì chỉ những hợp đồng có sự kiện hóa đơn liên quan mới được ghi nhận.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

##### **Truy xuất dữ liệu nguồn**

Bạn có thể tải dữ liệu ra để phân tích bên ngoài AWS Marketplace hoặc sử dụng với các công cụ khác. Để xuất dữ liệu:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

1. Sử dụng bộ lọc ở đầu trang để thu hẹp dữ liệu.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

2. Ở góc trên bên phải của bảng, chọn biểu tượng tùy chọn bổ sung (biểu tượng ba chấm dọc).[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

3. Chọn tùy chọn xuất dữ liệu.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Ảnh chụp màn hình sau đây hiển thị chế độ xem **Phân tích chi phí** của bảng điều khiển Procurement Insights.

#### **Chế độ xem Hợp đồng**

Tab **Agreements** hiển thị tất cả hợp đồng của bạn, bao gồm cả những hợp đồng đang hoạt động và đã hết hạn. Sử dụng chế độ xem này để theo dõi khi nào các hợp đồng hết hạn và hiểu cách tổ chức của bạn sử dụng các hợp đồng AWS Marketplace theo thời gian. Các hợp đồng đã hết hạn chỉ được theo dõi từ thời điểm tính năng được kích hoạt.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Lọc hợp đồng bằng các tùy chọn sau:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Ngày kết thúc hợp đồng** – Lọc hợp đồng theo ngày kết thúc.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Pay-as-you-go** – Bao gồm hoặc loại khỏi các hợp đồng pay-as-you-go trong các tùy chọn hàng năm và hợp đồng.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Loại đề nghị** – Lọc theo loại đề nghị, như đề nghị riêng tư hoặc công khai.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Phần **Active agreements** hiển thị tổng số hợp đồng hiện tại.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Phần **Expired agreements** hiển thị tổng số hợp đồng không còn hoạt động.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Chế độ xem **Agreements** của bảng điều khiển Procurement insights cung cấp nhiều cách để trực quan hóa dữ liệu của bạn. Biểu đồ **Agreements by days until expiration** cho thấy có bao nhiêu hợp đồng sẽ hết hạn trong các khoảng thời gian khác nhau.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Phần **New agreements trend** hiển thị đường xu hướng để hình dung khi nào tổ chức của bạn ký các hợp đồng theo thời gian.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

##### **Truy xuất dữ liệu nguồn**

Tải xuống dữ liệu để phân tích bên ngoài AWS Marketplace hoặc sử dụng với các công cụ khác. Để xuất dữ liệu, hãy thực hiện như sau:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

1. Sử dụng các bộ lọc ở đầu trang để tinh chỉnh dữ liệu.

2. Ở góc trên bên phải của biểu đồ, chọn biểu tượng tùy chọn bổ sung (ba chấm).

3. Chọn xuất dữ liệu.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Bảng điều khiển AWS Marketplace Procurement Insights hiển thị các thỏa thuận đang hoạt động và đã hết hạn, phân bố thời gian hết hạn thỏa thuận, xu hướng thỏa thuận mới, và các chỉ số thỏa thuận ở cấp độ sản phẩm.

![Enter image alt description](/images/3-Blog/blog2_figure3.png)

*Hình 3: Bảng điều khiển AWS Marketplace Procurement Insights – Agreement Metrics với các hợp đồng đang hoạt động, xu hướng hết hạn, và phân tích theo sản phẩm.*

**Truy cập dữ liệu thỏa thuận**

Để xem và xuất dữ liệu thỏa thuận AWS Marketplace của tổ chức bạn từ bất kỳ tiện ích nào trên bảng điều khiển:

1. Ở góc trên bên phải của biểu đồ, chọn biểu tượng tùy chọn bổ sung (được biểu thị bằng ba dấu chấm dọc).

2. Chọn tùy chọn xuất dữ liệu.

##### **Xem dữ liệu tóm tắt**

Nhanh chóng xem những thông tin tổng hợp liên quan đến các hợp đồng hiển thị trong biểu đồ bằng tùy chọn **View summary data**. Chế độ xem tóm tắt này cung cấp một phân tích cô đọng, bao gồm các chi tiết như tổng số hợp đồng trong các khoảng ngày hết hạn khác nhau, các chỉ số chính cho quản lý hợp đồng, và các loại hợp đồng cụ thể (như đề nghị riêng tư hoặc công khai).[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Bằng cách xem dữ liệu tóm tắt, bạn có thể nhận ra các mô hình, như nhiều hợp đồng sắp hết hạn, điều này giúp thúc đẩy việc đàm phán sớm hoặc thảo luận gia hạn với nhà cung cấp.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Xuất dữ liệu hợp đồng trực tiếp ra file CSV bằng tùy chọn **Export to CSV**, giúp bạn dễ dàng phân tích, báo cáo hoặc tích hợp với các hệ thống quản lý tài sản hoặc mua sắm khác.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)Bạn có thể kết hợp dữ liệu chi tiêu AWS Marketplace với các chi phí phần mềm khác để:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- Tìm cách giảm chi tiêu.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- Xác định các giấy phép phần mềm mà bạn có thể gộp lại.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- Lập kế hoạch ngân sách phần mềm hiệu quả hơn.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Điều này đặc biệt có lợi cho các tổ chức lớn quản lý nhiều tài khoản AWS. Các bộ phận CNTT và tài chính sử dụng tính năng xuất này để đưa dữ liệu AWS Marketplace vào các công cụ theo dõi tài sản hoặc lập ngân sách rộng hơn, từ đó hỗ trợ lập kế hoạch tài chính và quản lý nhà cung cấp tốt hơn.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)File CSV xuất ra bao gồm các trường quan trọng như:[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Account ID** – Xác định tài khoản AWS nào hợp đồng được liên kết.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Tên sản phẩm** – Phần mềm cụ thể, dịch vụ chuyên môn hoặc bộ dữ liệu từ AWS Marketplace.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Nhà cung cấp và loại đề nghị** – Thông tin về nhà cung cấp và liệu đó là đề nghị riêng tư hay công khai.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

- **Ngày bắt đầu và kết thúc hợp đồng** – Cho biết khi nào hợp đồng bắt đầu và kết thúc.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

**Điều khoản và lịch thanh toán** – Bao gồm chi tiết thanh toán như trạng thái pay-as-you-go hoặc các khoản thanh toán theo lịch trình.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Biểu đồ từ bảng điều khiển Procurement insights hiển thị số hợp đồng theo subscriber account ID và theo sản phẩm, bao gồm các nhà cung cấp hàng đầu.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

![Enter image alt description](/images/3-Blog/blog2_figure4.png)

*Hình 4: Các thỏa thuận theo Tài khoản người đăng ký (Subscriber Account) và Sản phẩm (Product) trong bảng điều khiển AWS Marketplace Procurement Insights.*

### **Bảng điều khiển này khác với các công cụ AWS khác như thế nào?**

AWS cung cấp nhiều công cụ quản trị, nhưng bảng điều khiển Procurement insights nổi bật bằng cách cung cấp các tính năng đặc thù dành riêng cho khách hàng AWS Marketplace mà không tốn thêm chi phí, và không yêu cầu sử dụng hoặc phí từ các dịch vụ AWS khác để cung cấp toàn bộ chức năng của nó.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Ngược lại, [AWS Billing](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-getting-started.html) và Cost Management hiển thị các khoản chi hoặc dòng mục khi việc sử dụng phần mềm phát sinh phí, nhưng không bao gồm chi tiết hợp đồng.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)Tương tự, AWS Cost Management cung cấp các chi tiết cấp cao (ví dụ: tên sản phẩm, chi phí phát sinh), nhưng không bao gồm dữ liệu hợp đồng AWS Marketplace.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

Đối với khách hàng không sử dụng AWS console, [Single Pane of Glass (SPG) dashboard](https://aws.amazon.com/blogs/awsmarketplace/visualizing-third-party-software-license-procurement-with-aws-marketplace-single-pane-of-glass-dashboard/), yêu cầu giấy phép [AWS QuickSight](https://aws.amazon.com/quicksight/), hợp nhất dữ liệu từ [AWS Cost and Usage Reports (CUR)](https://aws.amazon.com/aws-cost-management/aws-cost-and-usage-reporting/) và [AWS License Manager](https://aws.amazon.com/license-manager/). Mặc dù nó cung cấp khả năng nhìn toàn bộ chi phí, kiểm toán và giấy phép trên nhiều đơn vị tổ chức (OUs) bên ngoài AWS Management Console, nhưng nó không gắn dữ liệu này với chi tiết các hợp đồng AWS Marketplace.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

### **Kết luận**

Với bảng điều khiển Procurement insights, AWS Marketplace giới thiệu một công cụ mạnh mẽ cho các nhóm mua sắm để có được tính minh bạch và kiểm soát đối với tài sản phần mềm từ các ISV được mua qua AWS Marketplace trên toàn tổ chức. Nó đơn giản hóa phân tích chi phí và cung cấp khả năng nhìn nhận mô hình chi tiêu giúp hỗ trợ các quyết định mua sắm chiến lược.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

### **Tài nguyên**

- [Enabling the Procurement insights dashboard](https://docs.aws.amazon.com/marketplace/latest/buyerguide/enabling-procurement-insights.html)

- [Viewing cost reports with Procurement insights](https://docs.aws.amazon.com/marketplace/latest/buyerguide/procurement-insights.html)

- [Accessing the dashboard programmatically](https://docs.aws.amazon.com/marketplace/latest/buyerguide/management-access-with-apis.html)[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

### **Về các tác giả**

![Enter image alt description](/images/3-Blog/blog2_figure5.jpg)
Elhadj Barry là kiến trúc sư giải pháp chuyên về AWS Marketplace tại Washington DC, tập trung vào quản trị và bảo mật AWS Marketplace. Ông đam mê sử dụng các dịch vụ AWS để tạo ra các giải pháp đổi mới mang lại giá trị và kết quả kinh doanh.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

![Enter image alt description](/images/3-Blog/blog2_figure6.jpg)
[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)Atif Saeed là quản lý sản phẩm cao cấp tại AWS Marketplace, tập trung vào cải thiện trải nghiệm mua hàng và giúp các tổ chức tối ưu hóa đầu tư phần mềm ISV của họ. Qua công việc của mình, Atif hướng đến cung cấp cho khách hàng các hiểu biết tốt hơn trong quá trình mua sắm, đơn giản hóa quản lý giấy phép và giúp tạo ra giá trị lớn hơn từ các giao dịch phần mềm qua AWS Marketplace.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)[ \
](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)

![Enter image alt description](/images/3-Blog/blog2_figure7.jpg)
Juan Palazuelos là kỹ sư phát triển phần mềm cao cấp, đã phát hành hai dịch vụ AWS Marketplace công khai. Juan tập trung xây dựng các giải pháp có khả năng mở rộng để nâng cao trải nghiệm khách hàng AWS Marketplace.[ ](https://aws.amazon.com/vi/blogs/awsmarketplace/how-to-get-organization-wide-visibility-into-aws-marketplace-purchases/)
