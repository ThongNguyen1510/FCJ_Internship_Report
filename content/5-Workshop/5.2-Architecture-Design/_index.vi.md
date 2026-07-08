---
title: "Kiến trúc & Thiết kế kỹ thuật"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---


### 1. Sơ đồ kiến trúc (Architecture Diagram)

![Architecture Diagram](/images/5-Workshop/architecture_diagram.png)

```mermaid
flowchart TD
    subgraph AWS_Cloud ["☁️ AWS Cloud (Serverless Environment)"]
        direction TB
        
        subgraph Trigger_Layer ["1. Trigger Layer"]
            EB["⏱️ Amazon EventBridge<br/>(Cron Rule: rate(5 mins))"]
        end
        
        subgraph Compute_Layer ["2. Compute & Security Layer"]
            LAMBDA["⚡ AWS Lambda<br/>(Python 3.12)"]
            IAM["🔐 IAM Role<br/>(Least Privilege)"]
            IAM -.->|Grants access| LAMBDA
        end
        
        subgraph Storage_Alert_Layer ["3. Storage & Alert Layer"]
            DDB[("🗄️ Amazon DynamoDB<br/>(Table: WebsiteMonitorLogs)")]
            SNS["📧 Amazon SNS<br/>(Topic: Website-Alert-Topic)"]
        end
        
        subgraph Monitoring_Layer ["4. Monitoring Layer"]
            CW["📜 Amazon CloudWatch<br/>(Logs & Metrics)"]
        end
        
        EB == "1. Trigger" ==> LAMBDA
        LAMBDA == "3. Ghi Lịch sử" ==> DDB
        LAMBDA == "4. Bắn Alert nếu Lỗi" ==> SNS
        LAMBDA -. "Ghi Log" .-> CW
    end

    TARGET(("🌐 Website Mục Tiêu"))
    ADMIN["👨‍💻 SysAdmin"]

    LAMBDA == "2. HTTP GET (Timeout 5s)" ==> TARGET
    TARGET -. "HTTP Status & Latency" .-> LAMBDA
    SNS == "5. Gửi Email Notification" ==> ADMIN

    style AWS_Cloud fill:#f9f9f9,stroke:#ff9900,stroke-width:2px,color:#000
    style Trigger_Layer fill:#e1f5fe,stroke:#03a9f4,stroke-width:1px
    style Compute_Layer fill:#fff3e0,stroke:#ff9800,stroke-width:1px
    style Storage_Alert_Layer fill:#e8f5e9,stroke:#4caf50,stroke-width:1px
    style Monitoring_Layer fill:#fce4ec,stroke:#e91e63,stroke-width:1px
```

### 2. Lựa chọn dịch vụ & Lý do
1.  **Amazon EventBridge (Cronjob):** Không mất phí chạy EC2 24/7 để làm máy chủ chạy cronjob. EventBridge kích hoạt chính xác theo lịch trình.
2.  **AWS Lambda (Compute):** Thực thi code Python nhanh gọn (~1s). Tiết kiệm chi phí vì chỉ tính tiền lúc code chạy.
3.  **Amazon DynamoDB (Database):** Serverless NoSQL, tốc độ ghi siêu nhanh, thiết kế theo chuẩn dạng chuỗi thời gian (Time-series).
4.  **Amazon SNS (Alerting):** Tích hợp sẵn gửi thông báo Email đơn giản mà không cần cấu hình Mail Server.
5.  **Terraform (IaC):** Tự động hóa tạo tài nguyên nhanh chóng, dễ dàng dựng/hủy tài nguyên sạch sẽ.

> [!IMPORTANT]
> **Bảo mật & IAM:** Tuân thủ **Principle of Least Privilege**. Hàm Lambda KHÔNG dùng quyền Administrator, mà được cấp một IAM Role chỉ có đúng 3 quyền: Ghi log (`logs:PutLogEvents`), Ghi database (`dynamodb:PutItem`), Gửi thông báo (`sns:Publish`). Không hard-code credentials.
