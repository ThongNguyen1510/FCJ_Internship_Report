---
title: "Test & Validation"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---


To verify that the serverless telemetry monitoring workflow runs correctly, we run tests on execution logging and database entry creations.

### 1. Manual Invocation & Log Analysis
To trigger a validation ping immediately, execute the Lambda function using the AWS CLI command:
```bash
aws lambda invoke --function-name WebsiteMonitorFunction response.json
```

Open the AWS Console, locate `CloudWatch` > `Log Groups` > `/aws/lambda/WebsiteMonitorFunction` to review the execution statistics:
![CloudWatch Execution Logs](/images/5-Workshop/cloudwatch_logs.png)

These logs detail the run duration (`Duration`), the runtime size (`Memory Size`), and initialization times.

### 2. Verify Database Records
Access the `DynamoDB` console and choose the `WebsiteMonitorLogs` table. Use the `Explore items` view to review recorded pings:
![DynamoDB Log Records](/images/5-Workshop/dynamodb_records.png)

Each entry contains the monitored `url`, the timestamp (`timestamp`), the success flag (`is_up`), response latency (`response_time_ms`), and the returned HTTP status code (`status_code`).

### 3. Failure Mode Simulation
To simulate a website failure and test the alerting email functionality:
1. Update `target_url` in `main.tf` to an invalid URL, e.g. `default = "https://www.google.com/link-bi-loi-404"`.
2. Apply the change: `terraform apply`.
3. Trigger a manual check: `aws lambda invoke --function-name WebsiteMonitorFunction response.json`.
4. Validate that you instantly receive a notification email warning of the HTTP 404 failure.
