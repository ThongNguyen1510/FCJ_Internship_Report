---
title: "Clean up"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---


To remove all the resources deployed during the workshop (Lambda function, DynamoDB table, EventBridge rule, SNS topic, and IAM policies), execute the command below in your terminal:

```bash
terraform destroy
```

Type `yes` when prompted and press Enter. Terraform will cleanly delete all created resources to prevent any unexpected costs.
