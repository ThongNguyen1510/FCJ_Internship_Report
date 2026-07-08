---
title: "Appendix: Least Privilege IAM Policy"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---


Instead of allocating administrator credentials (`AdministratorAccess`) to your Terraform environment, assign this custom IAM policy to limit resource permissions specifically to this project's requirements:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowTerraformDynamoDB",
            "Effect": "Allow",
            "Action": [
                "dynamodb:CreateTable",
                "dynamodb:DeleteTable",
                "dynamodb:DescribeTable",
                "dynamodb:ListTagsOfResource",
                "dynamodb:TagResource"
            ],
            "Resource": "arn:aws:dynamodb:*:*:table/WebsiteMonitorLogs"
        },
        {
            "Sid": "AllowTerraformLambda",
            "Effect": "Allow",
            "Action": [
                "lambda:CreateFunction",
                "lambda:DeleteFunction",
                "lambda:GetFunction",
                "lambda:GetFunctionConfiguration",
                "lambda:AddPermission",
                "lambda:RemovePermission"
            ],
            "Resource": "arn:aws:lambda:*:*:function:WebsiteMonitorFunction"
        },
        {
            "Sid": "AllowTerraformSNS",
            "Effect": "Allow",
            "Action": [
                "sns:CreateTopic",
                "sns:DeleteTopic",
                "sns:GetTopicAttributes",
                "sns:Subscribe",
                "sns:Unsubscribe",
                "sns:ListTagsForResource",
                "sns:TagResource"
            ],
            "Resource": "arn:aws:sns:*:*:Website-Alert-Topic"
        },
        {
            "Sid": "AllowTerraformEventBridge",
            "Effect": "Allow",
            "Action": [
                "events:PutRule",
                "events:DeleteRule",
                "events:DescribeRule",
                "events:PutTargets",
                "events:RemoveTargets",
                "events:ListTagsForResource"
            ],
            "Resource": "arn:aws:events:*:*:rule/every-5-minutes-monitor"
        },
        {
            "Sid": "AllowTerraformIAMRole",
            "Effect": "Allow",
            "Action": [
                "iam:CreateRole",
                "iam:DeleteRole",
                "iam:GetRole",
                "iam:PassRole",
                "iam:CreatePolicy",
                "iam:DeletePolicy",
                "iam:GetPolicy",
                "iam:GetPolicyVersion",
                "iam:AttachRolePolicy",
                "iam:DetachRolePolicy",
                "iam:ListInstanceProfilesForRole",
                "iam:ListRolePolicies",
                "iam:ListAttachedRolePolicies"
            ],
            "Resource": [
                "arn:aws:iam::*:role/LambdaMonitorRole",
                "arn:aws:iam::*:policy/LambdaMonitorPolicy"
            ]
        }
    ]
}
```
