---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Dịch các bài blog kỹ thuật và thiết lập luồng xử lý dữ liệu serverless.
* Viết hàm Lambda để xử lý gói tin IoT.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Dịch Blog 4: 'Triển khai kiểm soát truy cập chi tiết với Amazon Cognito'. | 25/05/2026 | 25/05/2026 | [Blog 4](3-BlogsTranslated/3.4-Blog4/) |
| 3 | Tạo S3 raw bucket lưu trữ thô và viết AWS IoT Core Rule để chuyển hướng dữ liệu. | 26/05/2026 | 26/05/2026 | <https://docs.aws.amazon.com/iot/> |
| 4 | Lập trình hàm AWS Lambda (Node.js) để bóc tách, chuẩn hóa và kiểm tra dữ liệu telemetry. | 27/05/2026 | 27/05/2026 | <https://docs.aws.amazon.com/lambda/> |
| 5 | Cung cấp endpoint gọi API từ bên ngoài bằng Amazon API Gateway. | 28/05/2026 | 28/05/2026 | <https://docs.aws.amazon.com/apigateway/> |
| 6 | Kiểm thử tích hợp: ESP32 gửi dữ liệu -> lưu S3 -> Lambda tự động kích hoạt. | 29/05/2026 | 29/05/2026 |  |


### Kết quả đạt được trong tuần 6:

* Hoàn thành bản dịch Blog 4.
* Triển khai thành công luồng xử lý tự động từ IoT Core tới S3 và Lambda.
