---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Nghiên cứu chuyên đề Tối ưu hóa hệ thống AWS - phần Tối ưu hóa chi phí (Cost Optimization).
* Thiết lập cấu hình mạng riêng tư bảo mật bằng VPC Endpoint cho dự án giám sát website.
* Thực hiện kiểm thử định tuyến mạng nội bộ.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Nghiên cứu tối ưu hóa chi phí: 'Cost Savings with Savings Plans and Reserved Instances' và 'Cost Visualization and Analytics'. | 29/06/2026 | 29/06/2026 | <https://docs.aws.amazon.com/cost-management/> |
| 3 | Học cách phân tích dữ liệu lớn chi phí thấp bằng 'Cost Data Analysis with AWS Glue and Amazon Athena'. | 30/06/2026 | 30/06/2026 | <https://docs.aws.amazon.com/athena/> |
| 4 | Triển khai VPC Gateway Endpoint cho Amazon S3 và DynamoDB trong VPC để hàm Lambda (ở Private Subnet) truy cập trực tiếp các dịch vụ này không cần đi qua internet. | 01/07/2026 | 01/07/2026 | <https://docs.aws.amazon.com/vpc/> |
| 5 | Cấu hình Endpoint Policy nhằm giới hạn quyền truy cập S3/DynamoDB từ mạng nội bộ, ngăn ngừa rò rỉ dữ liệu. | 02/07/2026 | 02/07/2026 | <https://docs.aws.amazon.com/vpc/> |
| 6 | Kích hoạt VPC Flow Logs và kiểm tra định tuyến đảm bảo các kết nối của hệ thống giám sát đều đi qua đường truyền private. | 03/07/2026 | 03/07/2026 | <https://docs.aws.amazon.com/vpc/> |

### Kết quả đạt được trong tuần 11:

* Hiểu rõ cách phân tích chi phí bằng Cost Explorer, tối ưu bằng Savings Plans.
* Bảo mật thành công hệ thống giám sát bằng cách cô lập hoàn toàn luồng truyền dữ liệu của Lambda vào mạng riêng ảo qua VPC Endpoints.
