---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Tham gia Event 2 và chuyển đổi toàn bộ hạ tầng đã tạo thủ công sang mã Terraform HCL.
* Thiết lập các biến cấu hình dự án linh hoạt.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Xây dựng cấu trúc thư mục code Terraform: Khai báo AWS Provider (`main.tf`) và viết các biến đầu vào (`variables.tf`). | 15/06/2026 | 15/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| 3 | Viết mã Terraform định nghĩa các tài nguyên AWS: Lambda, DynamoDB, SNS Topic và EventBridge Rules. | 16/06/2026 | 16/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| 4 | Tham gia Event 2 (FCAJ Community Day - Conference Call) tìm hiểu multi-agent, CloudFront, LLM non-determinism. | 17/06/2026 | 17/06/2026 | [](4-EventParticipated/4.2-Event2/) |
| 5 | Sử dụng nguồn dữ liệu `archive_file` trong Terraform để tự động nén thư mục code Python của Lambda. | 18/06/2026 | 18/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| 6 | Định nghĩa IAM Role và IAM Policy gán quyền ghi bảng DynamoDB và đăng bài SNS cho Lambda bằng Terraform. | 19/06/2026 | 19/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |

### Kết quả đạt được trong tuần 9:

* Tham gia Event 2 và rút ra nhiều kinh nghiệm quý báu.
* Hoàn thành bản thảo mã nguồn Terraform đầy đủ cho toàn bộ hạ tầng giám sát website.
