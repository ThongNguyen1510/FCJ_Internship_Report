---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Dịch blog công nghệ được giao.
* Tích hợp dịch vụ tin nhắn Amazon SNS gửi email cảnh báo tự động khi website bị sập.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Dịch Blog 5: 'Xây dựng quy trình xử lý dữ liệu quy mô lớn cho IoT Analytics'. | 01/06/2026 | 01/06/2026 | [](3-BlogsTranslated/3.5-Blog5/) |
| 3 | Tìm hiểu Amazon SNS (Simple Notification Service) và các phương thức thông báo (Email, SMS, HTTPS). | 02/06/2026 | 02/06/2026 | <https://docs.aws.amazon.com/sns/> |
| 4 | Tạo một SNS Topic và đăng ký (Subscribe) bằng Email cá nhân, xác nhận đăng ký. | 03/06/2026 | 03/06/2026 | <https://docs.aws.amazon.com/sns/> |
| 5 | Bổ sung logic trong hàm Lambda: kiểm tra mã phản hồi HTTP, nếu khác 200 thì gọi API SNS gửi thông báo khẩn cấp. | 04/06/2026 | 04/06/2026 | <https://docs.aws.amazon.com/sns/> |
| 6 | Kiểm thử giả lập: cấu hình giám sát một trang web bị sập và kiểm tra nhận Email cảnh báo thành công. | 05/06/2026 | 05/06/2026 |  |

### Kết quả đạt được trong tuần 7:

* Hoàn thành bản dịch Blog 5 chất lượng.
* Tích hợp thành công luồng cảnh báo lỗi website thời gian thực, nhận email cảnh báo trong vòng 1 phút.
