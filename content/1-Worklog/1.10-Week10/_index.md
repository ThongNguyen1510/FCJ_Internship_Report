---
title: "Worklog Week 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Goals:

* Execute the Terraform build, verify alarms, and configure billing safeguards.
* Complete operational guides and enable logging analytics.

### Tasks implemented this week:
| Day | Task | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| Mon | Initialize the state backend (`terraform init`) and execute dry-runs (`terraform plan`) to audit resource paths. | 22/06/2026 | 22/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| Tue | Deploy the infrastructure by running `terraform apply` to establish the serverless monitoring loop. | 23/06/2026 | 23/06/2026 | <https://developer.hashicorp.com/terraform/tutorials> |
| Wed | Create CloudWatch Alarms targeted at Lambda execution metrics to flag internal script errors. | 24/06/2026 | 24/06/2026 | <https://docs.aws.amazon.com/AmazonCloudWatch/> |
| Thu | Configure AWS Budgets thresholds to email warning alerts if usage costs near Free Tier boundaries. | 25/06/2026 | 25/06/2026 | <https://docs.aws.amazon.com/awsaccountbilling/> |
| Fri | Document instructions for testing site failures, querying logs, and interpreting alert emails. | 26/06/2026 | 26/06/2026 |  |

### Week 10 Achievements:

* Automated the end-to-end serverless website monitor setup with a single CLI command.
* Configured operational metrics logging and safety cost limits.
