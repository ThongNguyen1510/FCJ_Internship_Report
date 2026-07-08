---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Hệ thống giám sát Website tự động (Serverless) với Infrastructure as Code

### 1. Tóm tắt điều hành
Hệ thống giám sát Website tự động (Serverless) được thiết kế nhằm cung cấp khả năng theo dõi trạng thái và độ trễ thời gian thực cho các trang web quan trọng. Tận dụng hạ tầng AWS Serverless (Lambda, EventBridge, DynamoDB, SNS) và triển khai hoàn toàn bằng Terraform (IaC), giải pháp mang lại khả năng hoạt động không cần bảo trì, độ tin cậy cao, tối ưu chi phí (100% Free Tier) cùng cảnh báo email tức thì khi xảy ra sự cố.

### 2. Tuyên bố vấn đề
*   **Vấn đề hiện tại:** Các giải pháp giám sát website truyền thống thường yêu cầu duy trì các máy chủ giám sát chuyên dụng (ví dụ: máy ảo, máy chủ EC2) chạy 24/7, phát sinh chi phí vận hành liên tục và tốn công bảo trì hệ điều hành, cập nhật bảo mật. Mặt khác, các dịch vụ giám sát SaaS bên thứ ba thường đắt đỏ và bị giới hạn tính năng ở phiên bản miễn phí.
*   **Giải pháp đề xuất:** Một kiến trúc hoàn toàn serverless, trong đó quy tắc EventBridge kích hoạt hàm Lambda nhẹ mỗi 5 phút để ping kiểm tra website mục tiêu. Thời gian phản hồi và mã trạng thái được ghi lại trong Amazon DynamoDB phục vụ tra cứu lịch sử, trong khi Amazon SNS gửi thông báo email tức thời nếu phát hiện lỗi HTTP (như 404, 500) hoặc lỗi kết nối.
*   **Lợi ích & ROI:** Loại bỏ hoàn toàn hóa đơn duy trì máy chủ với giải pháp nằm trọn trong AWS Free Tier. Triển khai tức thì bằng Terraform giúp đồng nhất môi trường và dễ dàng nâng cấp. Giảm tải công việc giám sát thủ công cho SysAdmin nhờ khả năng phát hiện và cảnh báo sự cố dưới 1 phút.

### 3. Kiến trúc giải pháp
Giải pháp áp dụng mô hình Serverless để đảm bảo tính sẵn sàng cao và không tốn công vận hành. Các thành phần hạ tầng bao gồm:
*   **Amazon EventBridge:** Kích hoạt hàm kiểm tra theo chu kỳ cron (`rate(5 minutes)`).
*   **AWS Lambda (Python 3.12):** Thực hiện gửi request kiểm tra URL, đo lường độ trễ và ghi dữ liệu.
*   **Amazon DynamoDB:** Lưu trữ lịch sử dạng chuỗi thời gian (`WebsiteMonitorLogs`).
*   **Amazon SNS:** Gửi email thông báo sự cố tới quản trị viên (`Website-Alert-Topic`).
*   **Amazon CloudWatch:** Ghi nhận log thực thi và giám sát hoạt động hệ thống.
*   **Terraform:** Khởi tạo tự động toàn bộ hạ tầng bằng mã nguồn (IaC).

![Sơ đồ kiến trúc](/images/5-Workshop/architecture_diagram.png)

### 4. Triển khai kỹ thuật
**Các giai đoạn triển khai**
1.  **Thiết kế & Thiết lập:** Thiết kế logic cho hàm Lambda và xây dựng phân quyền IAM tối thiểu (Tháng 1).
2.  **Viết mã Terraform:** Xây dựng các file cấu hình HCL cho DynamoDB, Lambda, SNS, IAM và EventBridge (Tháng 2).
3.  **Kiểm thử & Tích hợp:** Thực thi Lambda thủ công, kiểm tra log trên CloudWatch, đối chiếu bảng DynamoDB và tạo lỗi giả lập 404 để xác thực email cảnh báo (Tháng 2-3).
4.  **Vận hành tự động:** Chạy trigger tự động theo chu kỳ mỗi 5 phút trên môi trường production (Tháng 3).

**Yêu cầu kỹ thuật**
*   **Máy cá nhân:** Cài đặt sẵn AWS CLI và Terraform.
*   **Tài khoản AWS:** Tài khoản Free Tier đã cấu hình Access Key có quyền phù hợp.

### 5. Lộ trình & Mốc triển khai
*   **Tháng 1:** Học nền tảng AWS Serverless, phát triển hàm Lambda bằng Python và cấu hình môi trường AWS CLI cá nhân.
*   **Tháng 2:** Thiết lập mã nguồn Terraform (`main.tf`), thực hiện khởi tạo hạ tầng và xác thực các tài nguyên được tạo thành công.
*   **Tháng 3:** Kiểm thử liên thông toàn hệ thống, ghi nhận lịch sử hoạt động, kiểm tra gửi email cảnh báo, viết báo cáo và dọn dẹp tài nguyên.

### 6. Ước tính ngân sách
*   **Chi phí vận hành:** 0.00 USD / tháng (100% nằm trong định mức AWS Free Tier).
    *   *EventBridge:* 8,640 lần kích hoạt/tháng (Free Tier miễn phí 1 triệu lần/tháng).
    *   *Lambda:* 8,640 request/tháng * 1s thực thi (Free Tier miễn phí 1 triệu request & 400.000 GB-giây/tháng).
    *   *DynamoDB:* 8,640 lượt ghi/tháng (Free Tier miễn phí 25 GB lưu trữ và 25 WCU/RCU).
    *   *SNS:* Khoảng 10 email cảnh báo/tháng (Free Tier miễn phí 1.000 email thông báo/tháng).
    *   *CloudWatch Logs:* Khoảng 50 MB log/tháng (Free Tier miễn phí 5 GB ghi log/tháng).
*   **Chi phí phần cứng:** 0.00 USD (Không cần thiết bị phần cứng).

### 7. Đánh giá rủi ro
**Ma trận rủi ro**
*   **Email cảnh báo bị trễ hoặc vào thư rác:** Ảnh hưởng cao, xác suất thấp. *Biện pháp:* Thêm tên miền SNS của AWS vào danh sách tin cậy, kiểm tra hộp thư rác và xác nhận trạng thái Subscription của SNS.
*   **Bị chặn IP bởi WAF/Rate Limit:** Ảnh hưởng trung bình, xác suất thấp. *Biện pháp:* Cấu hình User-Agent thực tế cho request của Lambda hoặc thêm dải IP của AWS Lambda vào danh sách trắng của máy chủ mục tiêu.
*   **Phát sinh chi phí ngoài ý muốn:** Ảnh hưởng trung bình, xác suất thấp. *Biện pháp:* Cài đặt AWS Budgets để cảnh báo khi chi phí vượt quá 1 USD.

### 8. Kết quả kỳ vọng
*   Triển khai hạ tầng tự động hóa 100% qua mã nguồn Terraform.
*   Dữ liệu lịch sử đo lường trạng thái được lưu trữ an toàn trong NoSQL database.
*   Thời gian phát hiện và gửi email cảnh báo dưới 1 phút khi website gặp sự cố.
*   Không cần bảo trì hệ thống giám sát và không phát sinh bất kỳ chi phí nào.
