---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Triển khai hạ tầng đám mây tự động bằng Terraform và cấu hình giám sát cảnh báo.
* Thiết lập hệ thống kiểm soát chi phí đầu tư đám mây và viết tài liệu hướng dẫn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Chạy câu lệnh `terraform init` và `terraform plan` để kiểm tra logic hạ tầng trước khi khởi tạo. | 22/06/2026 | 22/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| 3 | Thực hiện `terraform apply` để triển khai toàn bộ hệ thống giám sát website tự động lên AWS. | 23/06/2026 | 23/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| 4 | Cấu hình cảnh báo CloudWatch Alarm giám sát số lượng lỗi (Errors metric) phát sinh khi Lambda thực thi. | 24/06/2026 | 24/06/2026 | <https://docs.aws.amazon.com/AmazonCloudWatch/> |
| 5 | Thiết lập cảnh báo ngân sách chi phí AWS Budgets để nhận cảnh báo email nếu hóa đơn vượt ngưỡng Free Tier. | 25/06/2026 | 25/06/2026 | <https://docs.aws.amazon.com/awsaccountbilling/> |
| 6 | Viết tài liệu kỹ thuật chi tiết hướng dẫn vận hành, kiểm tra hoạt động hệ thống qua nhật ký CloudWatch Logs. | 26/06/2026 | 26/06/2026 |  |

### Kết quả đạt được trong tuần 10:

* Triển khai tự động hóa thành công toàn bộ hệ thống bằng Terraform.
* Thiết lập thành công cơ chế quản lý ngân sách và cảnh báo lỗi chủ động cho hệ thống.
