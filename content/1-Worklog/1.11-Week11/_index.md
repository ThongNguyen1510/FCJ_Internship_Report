---
title: "Worklog Week 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Goals:

* Study system optimization under the Cost Optimization pillar.
* Implement private VPC Endpoint connectivity to secure the website monitoring project.
* Validate internal routing paths in the private subnet.

### Tasks implemented this week:
| Day | Task | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| Mon | Study budget management: 'Cost Savings with Savings Plans and Reserved Instances' and 'Cost Visualization and Analytics'. | 29/06/2026 | 29/06/2026 | <https://docs.aws.amazon.com/cost-management/> |
| Tue | Study big data analysis: 'Cost Data Analysis with AWS Glue and Amazon Athena' to query logs cost-effectively. | 30/06/2026 | 30/06/2026 | <https://docs.aws.amazon.com/athena/> |
| Wed | Deploy VPC Gateway Endpoints for Amazon S3 and DynamoDB, allowing the Lambda function in the private subnet to connect securely without going through the internet. | 01/07/2026 | 01/07/2026 | <https://docs.aws.amazon.com/vpc/> |
| Thu | Configure custom VPC Endpoint Policies to restrict S3 and DynamoDB data access at the network boundary. | 02/07/2026 | 02/07/2026 | <https://docs.aws.amazon.com/vpc/> |
| Fri | Enable VPC Flow Logs and verify that the monitoring system's database logs route entirely through the private network endpoints. | 03/07/2026 | 03/07/2026 | <https://docs.aws.amazon.com/vpc/> |

### Week 11 Achievements:

* Understood AWS cost optimization strategies (RIs, Savings Plans) and Athena query mechanics.
* Secured the serverless monitoring loop by isolating Lambda network requests via private VPC Endpoints.
