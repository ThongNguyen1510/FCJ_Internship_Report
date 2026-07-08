---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Thực hiện kiểm thử tải và thắt chặt bảo mật cho backend serverless.
* Cấu hình cảnh báo ngân sách AWS Budget để quản lý chi phí.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Phân quyền chi tiết IAM policy cho các hàm Lambda và API Gateway. | 22/06/2026 | 22/06/2026 | <https://docs.aws.amazon.com/iam/> |
| 3 | Cấu hình AWS Budgets và CloudWatch Alarm để tự động gửi thông báo khi vượt ngưỡng chi phí. | 23/06/2026 | 23/06/2026 | <https://docs.aws.amazon.com/awsaccountbilling/> |
| 4 | Thực hiện giả lập tải cao để kiểm tra giới hạn (throttling) và xử lý lỗi của Lambda. | 24/06/2026 | 24/06/2026 |  |
| 5 | Cấu hình bộ đệm lưu trữ dữ liệu cục bộ trên Docker của thiết bị biên Raspberry Pi đề phòng mất mạng. | 25/06/2026 | 25/06/2026 |  |
| 6 | Viết tài liệu kỹ thuật chi tiết hướng dẫn vận hành mã nguồn thiết bị biên. | 26/06/2026 | 26/06/2026 |  |


### Kết quả đạt được trong tuần 10:

* Tăng cường tính an toàn cho hệ thống và kiểm soát chi phí tự động.
* Hoàn thành các bài kiểm tra tải hoạt động ổn định cho các API telemetry.
