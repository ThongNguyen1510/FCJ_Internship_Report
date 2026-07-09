---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Dịch bài blog kỹ thuật cuối cùng (Blog 6).
* Nghiên cứu các dịch vụ bảo vệ ứng dụng (WAF, GuardDuty, Firewall Manager) và phân quyền bảo mật.
* Xây dựng khung mã nguồn Lambda ping website và ghi lịch sử DynamoDB.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Dịch Blog 6: 'Bảo mật tích hợp API trong môi trường Hybrid Cloud'. | 08/06/2026 | 08/06/2026 | [](3-BlogsTranslated/3.6-Blog6/) |
| 3 | Nghiên cứu bài lab: 'Private Access to S3 with VPC Endpoints' và giải pháp bảo vệ web bằng 'Application Protection with AWS WAF'. | 09/06/2026 | 09/06/2026 | <https://docs.aws.amazon.com/waf/> |
| 4 | Nghiên cứu các giải pháp quản lý mối đe dọa: 'Security Governance with AWS Firewall Manager' và 'Threat Detection with AWS GuardDuty'. | 10/06/2026 | 10/06/2026 | <https://docs.aws.amazon.com/guardduty/> |
| 5 | Tìm hiểu bài lab: 'Systems Patching with EC2 Image Builder' và hệ thống xác thực người dùng 'Cross-Domain Authentication with Amazon Cognito'. | 11/06/2026 | 11/06/2026 | <https://docs.aws.amazon.com/cognito/> |
| 6 | Viết mã nguồn Python hàm Lambda thực hiện ping URL, đo lường latency và kết nối thư viện `boto3` để lưu kết quả vào DynamoDB. | 12/06/2026 | 12/06/2026 |  |

### Kết quả đạt được trong tuần 8:

* Hoàn thành dịch đầy đủ toàn bộ 6 bài blog công nghệ được giao.
* Hiểu rõ vai trò của AWS WAF chống khai thác lỗ hổng và đã lập trình thành công logic cốt lõi của hàm Lambda giám sát website.
