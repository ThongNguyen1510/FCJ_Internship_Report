---
title: "Triển khai & Lab step-by-step"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---


### 3.1. Prerequisite (Điều kiện tiên quyết)
*   **Tài khoản AWS:** Cần có tài khoản AWS đang hoạt động (dùng Free Tier).
*   **Công cụ:** 
    *   **AWS CLI:** Cài đặt để giao tiếp với AWS. Chạy lệnh `aws configure` trong Terminal để nhập Access Key / Secret Key.
    *   **Terraform:** Download và cài đặt Terraform CLI trên máy tính.

### 3.2. Hướng dẫn chi tiết End-to-End

**Step 1: Tạo thư mục chứa Code (CLI Guide)**
Mở Terminal / Command Prompt và chạy lệnh:
```bash
mkdir aws-monitor-project
cd aws-monitor-project
```

**Step 2: Tạo code thực thi cho Lambda (Python)**
Tạo một file tên `lambda_function.py` và dán code sau vào:
```python
import urllib.request
import urllib.error
import boto3
import time
import os
from datetime import datetime

DYNAMODB_TABLE = os.environ['DYNAMODB_TABLE']
SNS_TOPIC_ARN = os.environ['SNS_TOPIC_ARN']
TARGET_URL = os.environ['TARGET_URL']

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table(DYNAMODB_TABLE)
sns = boto3.client('sns')

def lambda_handler(event, context):
    timestamp = datetime.utcnow().isoformat()
    status_code = 0
    is_up = False
    
    start_time = time.time()
    try:
        req = urllib.request.Request(TARGET_URL, method='GET')
        with urllib.request.urlopen(req, timeout=5) as response:
            status_code = response.getcode()
            is_up = (status_code == 200)
    except urllib.error.HTTPError as e:
        status_code = e.code
    except Exception as e:
        status_code = -1 # Lỗi mạng, timeout
        
    response_time_ms = int((time.time() - start_time) * 1000)
    
    # Ghi vào DynamoDB
    table.put_item(
        Item={
            'url': TARGET_URL,
            'timestamp': timestamp,
            'status_code': status_code,
            'response_time_ms': response_time_ms,
            'is_up': is_up
        }
    )
    
    # Gửi cảnh báo
    if not is_up:
        message = f"CẢNH BÁO: Website {TARGET_URL} đang gặp sự cố!\nThời gian: {timestamp}\nStatus Code: {status_code}\nResponse Time: {response_time_ms} ms."
        sns.publish(
            TopicArn=SNS_TOPIC_ARN,
            Subject=f"ALERT: Website Down ({TARGET_URL})",
            Message=message
        )
        
    return {'statusCode': 200, 'body': f'Checked {TARGET_URL} - Status: {status_code}'}
```

**Step 3: Khai báo hạ tầng bằng Terraform**
Tạo file `main.tf` và dán toàn bộ đoạn code sau (thay đổi Email nhận cảnh báo ở biến `alert_email` dòng số 7):
```hcl
provider "aws" {
  region = "ap-southeast-2"
}

# BIẾN (VARIABLES) - HÃY SỬA EMAIL DƯỚI ĐÂY
variable "alert_email" {
  default = "email-cua-ban@gmail.com" 
}
variable "target_url" {
  default = "https://www.google.com"
}

# DYNAMODB
resource "aws_dynamodb_table" "monitor_logs" {
  name           = "WebsiteMonitorLogs"
  billing_mode   = "PAY_PER_REQUEST"
  hash_key       = "url"
  range_key      = "timestamp"
  attribute { name = "url"; type = "S" }
  attribute { name = "timestamp"; type = "S" }
}

# SNS TOPIC
resource "aws_sns_topic" "alert_topic" {
  name = "Website-Alert-Topic"
}
resource "aws_sns_topic_subscription" "email_target" {
  topic_arn = aws_sns_topic.alert_topic.arn
  protocol  = "email"
  endpoint  = var.alert_email
}

# IAM
data "aws_iam_policy_document" "lambda_assume_role" {
  statement {
    actions = ["sts:AssumeRole"]
    principals { type = "Service"; identifiers = ["lambda.amazonaws.com"] }
  }
}
resource "aws_iam_role" "lambda_role" {
  name               = "LambdaMonitorRole"
  assume_role_policy = data.aws_iam_policy_document.lambda_assume_role.json
}
resource "aws_iam_policy" "lambda_policy" {
  name = "LambdaMonitorPolicy"
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      { Action = ["logs:*"], Effect = "Allow", Resource = "arn:aws:logs:*:*:*" },
      { Action = "dynamodb:PutItem", Effect = "Allow", Resource = aws_dynamodb_table.monitor_logs.arn },
      { Action = "sns:Publish", Effect = "Allow", Resource = aws_sns_topic.alert_topic.arn }
    ]
  })
}
resource "aws_iam_role_policy_attachment" "attach" {
  role       = aws_iam_role.lambda_role.name
  policy_arn = aws_iam_policy.lambda_policy.arn
}

# LAMBDA
data "archive_file" "lambda_zip" {
  type        = "zip"
  source_file = "lambda_function.py"
  output_path = "lambda_function.zip"
}
resource "aws_lambda_function" "monitor_lambda" {
  filename         = "lambda_function.zip"
  function_name    = "WebsiteMonitorFunction"
  role             = aws_iam_role.lambda_role.arn
  handler          = "lambda_function.lambda_handler"
  runtime          = "python3.12"
  source_code_hash = data.archive_file.lambda_zip.output_base64sha256
  environment {
    variables = {
      DYNAMODB_TABLE = aws_dynamodb_table.monitor_logs.name
      SNS_TOPIC_ARN  = aws_sns_topic.alert_topic.arn
      TARGET_URL     = var.target_url
    }
  }
}

# EVENTBRIDGE (CRONJOB)
resource "aws_cloudwatch_event_rule" "cron" {
  name                = "every-5-minutes-monitor"
  schedule_expression = "rate(5 minutes)"
}
resource "aws_cloudwatch_event_target" "trigger" {
  rule      = aws_cloudwatch_event_rule.cron.name
  target_id = "lambda"
  arn       = aws_lambda_function.monitor_lambda.arn
}
resource "aws_lambda_permission" "allow_cloudwatch" {
  statement_id  = "AllowExecutionFromCloudWatch"
  action        = "lambda:InvokeFunction"
  function_name = aws_lambda_function.monitor_lambda.function_name
  principal     = "events.amazonaws.com"
  source_arn    = aws_cloudwatch_event_rule.cron.arn
}
```

**Step 4: Thực thi triển khai End-to-End**
Từ Terminal, gõ lệnh để tải về các thư viện của Terraform:
```bash
terraform init
```
Sau đó gõ lệnh để tạo toàn bộ kiến trúc lên mây:
```bash
terraform apply
```
Hệ thống sẽ liệt kê bản thiết kế kế hoạch triển khai tài nguyên:
![Terraform Apply Plan](/images/5-Workshop/terraform_apply_plan.png)

Gõ `yes` và nhấn Enter để tiếp tục, màn hình hiển thị dòng thông báo hoàn tất:
![Terraform Apply Complete](/images/5-Workshop/terraform_apply_complete.png)

**Step 5: Xác nhận Đăng ký Email qua SNS**
Mở Hộp thư Email, tìm thư xác nhận từ AWS và bấm vào đường dẫn **Confirm subscription** để hoàn tất cấu hình cảnh báo.
![Email Subscription Confirmation](/images/5-Workshop/email_confirmation.png)
