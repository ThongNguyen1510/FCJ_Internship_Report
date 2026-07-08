---
title: "Thu dọn tài nguyên"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---


Để xóa toàn bộ các tài nguyên đám mây đã khởi tạo trong workshop (tránh phát sinh chi phí phát sinh ngoài ý muốn), hãy mở Terminal và thực thi lệnh sau:

```bash
terraform destroy
```

Nhập `yes` và bấm Enter. Terraform sẽ tự động dọn dẹp sạch sẽ toàn bộ tài nguyên (xóa Lambda, DynamoDB, EventBridge, SNS và IAM Roles).
