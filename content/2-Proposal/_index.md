---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Automated Serverless Website Monitoring with IaC (Terraform)

### 1. Executive Summary
The Automated Serverless Website Monitoring system is designed to provide real-time status and latency monitoring for critical websites. Leveraging AWS Serverless services (Lambda, EventBridge, DynamoDB, SNS) and deployed entirely using Terraform (Infrastructure as Code), the solution offers zero-maintenance, high-reliability, and cost-efficient monitoring (100% Free Tier) with instant email alerts.

### 2. Problem Statement
*   **Current Problem:** Traditional website monitoring solutions often require running dedicated monitoring servers (e.g., VMs, EC2 instances), incurring continuous 24/7 runtime costs and administrative overhead for OS patches and agent maintenance. Furthermore, third-party monitoring SaaS platforms are expensive and offer limited features under their free plans.
*   **Proposed Solution:** A completely serverless architecture where an EventBridge rule triggers a lightweight AWS Lambda function every 5 minutes to ping target websites. Response times and status codes are stored persistently in Amazon DynamoDB for history logging, while Amazon SNS sends out real-time email alerts in case of HTTP errors (like 404, 500) or network timeouts.
*   **Benefits & ROI:** Replaces continuous hosting bills with a 100% Free Tier solution. Deploys instantly using Terraform, ensuring consistent environments and ease of updates. Reduces SysAdmin monitoring workload by providing precise alerts within 1 minute of a downtime event.

### 3. Solution Architecture
The solution employs AWS Serverless services for high availability and zero operational overhead. The infrastructure components are:
*   **Amazon EventBridge:** Triggers the monitoring function on a cron schedule (`rate(5 minutes)`).
*   **AWS Lambda (Python 3.12):** Pings the target URL, measures response latency, and writes results to DynamoDB.
*   **Amazon DynamoDB:** Stores time-series latency logs (`WebsiteMonitorLogs`).
*   **Amazon SNS:** Publishes alerts to subscriber emails (`Website-Alert-Topic`).
*   **Amazon CloudWatch:** Gathers execution logs and runtime metrics.
*   **Terraform:** Automates the provisioning of all resources.

![Architecture Diagram](/images/5-Workshop/architecture_diagram.png)

### 4. Technical Implementation
**Implementation Phases**
1.  **Design & Setup:** Design the Lambda function logic and IAM Least Privilege policies (Month 1).
2.  **Terraform Coding:** Write HCL templates for DynamoDB, Lambda, SNS, IAM, and EventBridge (Month 2).
3.  **Testing & Integration:** Perform manual invokes, check CloudWatch logs, confirm DynamoDB writes, and trigger synthetic 404 errors to test email alarms (Months 2-3).
4.  **Production & Automation:** Deploy the cron trigger to run every 5 minutes in production (Month 3).

**Technical Requirements**
*   **Local machine:** AWS CLI and Terraform installed.
*   **Credentials:** AWS Free Tier account with programmatic Access Keys configured.

### 5. Timeline & Milestones
*   **Month 1:** Learn AWS Serverless fundamentals, write the Lambda logic in Python, and set up local AWS CLI credentials.
*   **Month 2:** Write the Terraform configurations (`main.tf`), deploy the infrastructure locally, and confirm resource provisioning.
*   **Month 3:** Perform end-to-end integration tests, record uptime history, test alert emails, write report, and clean up.

### 6. Budget Estimation
*   **Operational Cost:** $0.00 / month (100% covered by AWS Free Tier).
    *   *EventBridge:* 8,640 invocations/month (Free Tier allows 1M free/month).
    *   *Lambda:* 8,640 requests/month * 1s runtime (Free Tier allows 1M requests & 400,000 GB-seconds/month).
    *   *DynamoDB:* 8,640 writes/month (Free Tier allows 25 GB storage & 25 WCU/RCU free).
    *   *SNS:* ~10 alert emails/month (Free Tier allows 1,000 email notifications/month).
    *   *CloudWatch Logs:* ~50 MB/month (Free Tier allows 5 GB log ingestion/month).
*   **Hardware Cost:** $0.00 (No hardware required).

### 7. Risk Assessment
**Risk Matrix**
*   **Outage Email Delayed/Filtered:** High impact, low probability. *Mitigation:* Add SNS email domain to white-list, check Spam folder, verify SNS subscription confirmation.
*   **Rate Limiting/WAF Block:** Medium impact, low probability. *Mitigation:* Set realistic User-Agent headers in HTTP request or white-list Lambda source IP range on the target server.
*   **Accidental Spend:** Medium impact, low probability. *Mitigation:* Configure AWS Budgets with alerts at $1 limit.

### 8. Expected Outcomes
*   100% automated infrastructure management using Terraform.
*   Real-time status history recorded securely in a NoSQL database.
*   Under 1-minute alert notification delivery upon site failure.
*   Zero infrastructure maintenance and zero recurring costs.
