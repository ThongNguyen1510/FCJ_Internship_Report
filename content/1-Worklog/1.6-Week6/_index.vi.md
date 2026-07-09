---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Dịch blog công nghệ được giao tiếp theo.
* Đưa mã script kiểm tra website lên AWS Lambda và kết nối cơ sở dữ liệu lưu trữ DynamoDB.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Dịch Blog 4: 'Triển khai kiểm soát truy cập chi tiết với Amazon Cognito'. | 25/05/2026 | 25/05/2026 | [](3-BlogsTranslated/3.4-Blog4/) |
| 3 | Đóng gói mã Python ping website và đưa lên AWS Lambda, cấu hình các biến môi trường (URL cần ping). | 26/05/2026 | 26/05/2026 | <https://docs.aws.amazon.com/lambda/> |
| 4 | Nghiên cứu cơ sở dữ liệu NoSQL Amazon DynamoDB (Key-Value, Primary Keys, Read/Write capacities). | 27/05/2026 | 27/05/2026 | <https://docs.aws.amazon.com/amazondynamodb/> |
| 5 | Tạo bảng DynamoDB để ghi nhận lịch sử kiểm tra (các cột lưu: URL, Timestamp, Status, Latency). | 28/05/2026 | 28/05/2026 | <https://docs.aws.amazon.com/amazondynamodb/> |
| 6 | Sử dụng thư viện SDK `boto3` trong hàm Lambda để tự động ghi kết quả kiểm tra vào bảng DynamoDB. | 29/05/2026 | 29/05/2026 | <https://docs.aws.amazon.com/amazondynamodb/> |

### Kết quả đạt được trong tuần 6:

* Hoàn thành bản dịch Blog 4 chất lượng.
* Triển khai thành công luồng xử lý tự động từ hàm Lambda ghi nhận kết quả lưu vào cơ sở dữ liệu DynamoDB.
