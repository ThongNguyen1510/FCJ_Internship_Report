---
title: "Architecture & Technical Design"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---


### 1. Architectural Diagram

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
        LAMBDA == "3. Write History" ==> DDB
        LAMBDA == "4. Publish Alert on Error" ==> SNS
        LAMBDA -. "Write Logs" .-> CW
    end

    TARGET(("🌐 Target Website"))
    ADMIN["👨‍💻 SysAdmin"]

    LAMBDA == "2. HTTP GET (Timeout 5s)" ==> TARGET
    TARGET -. "HTTP Status & Latency" .-> LAMBDA
    SNS == "5. Send Email Notification" ==> ADMIN

    style AWS_Cloud fill:#f9f9f9,stroke:#ff9900,stroke-width:2px,color:#000
    style Trigger_Layer fill:#e1f5fe,stroke:#03a9f4,stroke-width:1px
    style Compute_Layer fill:#fff3e0,stroke:#ff9800,stroke-width:1px
    style Storage_Alert_Layer fill:#e8f5e9,stroke:#4caf50,stroke-width:1px
    style Monitoring_Layer fill:#fce4ec,stroke:#e91e63,stroke-width:1px
```

### 2. Service Selection & Rationale
1.  **Amazon EventBridge (Cronjob):** Serverless scheduler. Replaces continuous EC2 instances to eliminate 24/7 runtime billing.
2.  **AWS Lambda (Compute):** Executes lightweight Python code quickly (~1s) and incurs zero cost when inactive.
3.  **Amazon DynamoDB (Database):** Serverless NoSQL time-series data storage with fast writes.
4.  **Amazon SNS (Alerting):** Simple email delivery without configuring complex SMTP mail servers.
5.  **Terraform (IaC):** Streamlines infrastructure staging, updating, and dismantling.

> [!IMPORTANT]
> **Security & IAM (Least Privilege):** Follows the **Principle of Least Privilege**. The Lambda function is granted limited execution policies allowing only S3 log streaming (`logs:PutLogEvents`), DynamoDB table insertions (`dynamodb:PutItem`), and SNS messaging (`sns:Publish`). Credentials are not hard-coded.
