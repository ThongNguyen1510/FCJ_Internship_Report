---
title: "Implementation & Lab step-by-step"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---


### 3.1. Prerequisite
*   **AWS Account:** An active AWS Free Tier account.
*   **Tools:**
    *   **AWS CLI:** Configured locally (`aws configure`) with security-hardened IAM credentials.
    *   **Terraform:** CLI installed.

### 3.2. Step-by-Step Deployment

**Step 1: Create Project Directory**
```bash
mkdir aws-monitor-project
cd aws-monitor-project
```

**Step 2: Write Lambda Handler (`lambda_function.py`)**
Create `lambda_function.py` and input the following code:
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
        status_code = -1 # Network timeout/connection error
        
    response_time_ms = int((time.time() - start_time) * 1000)
    
    # Save log to DynamoDB
    table.put_item(
        Item={
            'url': TARGET_URL,
            'timestamp': timestamp,
            'status_code': status_code,
            'response_time_ms': response_time_ms,
            'is_up': is_up
        }
    )
    
    # Send alert if website is down
    if not is_up:
        message = f"ALERT: Website {TARGET_URL} is experiencing issues!\nTime: {timestamp}\nStatus Code: {status_code}\nResponse Time: {response_time_ms} ms."
        sns.publish(
            TopicArn=SNS_TOPIC_ARN,
            Subject=f"ALERT: Website Down ({TARGET_URL})",
            Message=message
        )
        
    return {'statusCode': 200, 'body': f'Checked {TARGET_URL} - Status: {status_code}'}
```

**Step 3: Define Infrastructure as Code (`main.tf`)**
Create `main.tf` with the configuration below (remember to replace the default email variables):
```hcl
provider "aws" {
  region = "ap-southeast-2"
}

variable "alert_email" {
  default = "your-email@gmail.com" 
}
variable "target_url" {
  default = "https://www.google.com"
}

# DynamoDB Table
resource "aws_dynamodb_table" "monitor_logs" {
  name           = "WebsiteMonitorLogs"
  billing_mode   = "PAY_PER_REQUEST"
  hash_key       = "url"
  range_key      = "timestamp"
  attribute { name = "url"; type = "S" }
  attribute { name = "timestamp"; type = "S" }
}

# SNS Alert Topic & Subscription
resource "aws_sns_topic" "alert_topic" {
  name = "Website-Alert-Topic"
}
resource "aws_sns_topic_subscription" "email_target" {
  topic_arn = aws_sns_topic.alert_topic.arn
  protocol  = "email"
  endpoint  = var.alert_email
}

# IAM Role & Policies
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

# Lambda Zip
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

# EventBridge Scheduler
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

**Step 4: Execute Terraform Deployments**
Initialize Terraform to pull dependency providers:
```bash
terraform init
```
Generate and run the execution plan:
```bash
terraform apply
```

Review the target deployment plan output in terminal:
![Terraform Apply Plan](/images/5-Workshop/terraform_apply_plan.png)

Once approved, input `yes`. The terminal will return execution logs:
![Terraform Apply Complete](/images/5-Workshop/terraform_apply_complete.png)

**Step 5: Confirm SNS Email Subscription**
Check your email inbox for the subscription confirmation message from AWS. Click **Confirm subscription**.
![Email Subscription Confirmation](/images/5-Workshop/email_confirmation.png)
