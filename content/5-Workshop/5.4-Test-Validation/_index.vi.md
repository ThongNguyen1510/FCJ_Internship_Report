---
title: "Kiểm thử & Đo lường"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---


Sau khi triển khai thành công, chúng ta cần xác thực luồng ghi nhận dữ liệu và cảnh báo sự cố hoạt động chính xác.

### 1. Gửi request thủ công & Xem Log
Để kích hoạt kiểm tra ngay lập tức mà không cần đợi chu kỳ 5 phút của EventBridge, hãy gõ lệnh kích hoạt thủ công qua AWS CLI:
```bash
aws lambda invoke --function-name WebsiteMonitorFunction response.json
```

Truy cập AWS Console > `CloudWatch` > `Log groups` > `/aws/lambda/WebsiteMonitorFunction` để kiểm tra logs hoạt động:
![CloudWatch Execution Logs](/images/5-Workshop/cloudwatch_logs.png)

Các dòng logs chi tiết thời gian chạy (`Duration`), dung lượng bộ nhớ sử dụng (`Memory Size`) và thông tin khởi chạy.

### 2. Kiểm tra dữ liệu DynamoDB
Truy cập AWS Console > `DynamoDB` > `Explore Items` > Chọn bảng `WebsiteMonitorLogs`:
![DynamoDB Log Records](/images/5-Workshop/dynamodb_records.png)

Bảng dữ liệu hiển thị lịch sử thời gian đo lường (`timestamp`), độ trễ phản hồi (`response_time_ms`), mã trạng thái (`status_code`) và cờ hoạt động (`is_up`) tương ứng của website.

### 3. Kiểm thử lỗi (Test Alert)
Để kiểm tra tính hoạt động của cảnh báo email tự động khi website gặp sự cố:
1. Mở file `main.tf`, sửa URL mặc định thành một URL bị lỗi (ví dụ: `default = "https://www.google.com/link-bi-loi-404"`).
2. Chạy lệnh cập nhật: `terraform apply`.
3. Ép chạy Lambda ngay lập tức bằng lệnh: `aws lambda invoke --function-name WebsiteMonitorFunction response.json`.
4. Hệ thống sẽ ghi nhận lỗi status 404 và ngay lập tức gửi một email cảnh báo chi tiết về sự cố vào hộp thư bạn đã đăng ký.
