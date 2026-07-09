---
title: "Worklog Week 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Goals:

* Translate the designated technical blog post.
* Migrate the site check script to AWS Lambda and configure Amazon DynamoDB for logging.

### Tasks implemented this week:
| Day | Task | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| Mon | Translate Blog 4: 'Fine-Grained Access Control with Amazon Cognito'. | 25/05/2026 | 25/05/2026 | [](3-BlogsTranslated/3.4-Blog4/) |
| Tue | Deploy the Python ping logic to AWS Lambda and define targeted websites using environment variables. | 26/05/2026 | 26/05/2026 | <https://docs.aws.amazon.com/lambda/> |
| Wed | Study Amazon DynamoDB NoSQL key-value patterns and partition/sort key designs. | 27/05/2026 | 27/05/2026 | <https://docs.aws.amazon.com/amazondynamodb/> |
| Thu | Create a DynamoDB table structured for metrics logs (URL, Timestamp, Status, Latency). | 28/05/2026 | 28/05/2026 | <https://docs.aws.amazon.com/amazondynamodb/> |
| Fri | Implement Python SDK `boto3` inside the Lambda code to write results to DynamoDB. | 29/05/2026 | 29/05/2026 | <https://docs.aws.amazon.com/amazondynamodb/> |

### Week 6 Achievements:

* Completed translation for Blog 4.
* Successfully established the Lambda-to-DynamoDB data logging integration.
