---
title: "Worklog Week 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Goals:

* Translate the designated technical blog post.
* Integrate Amazon SNS (Simple Notification Service) to send email alerts on site failures.

### Tasks implemented this week:
| Day | Task | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| Mon | Translate Blog 5: 'Building a Large-Scale Data Pipeline for IoT Analytics'. | 01/06/2026 | 01/06/2026 | [](3-BlogsTranslated/3.5-Blog5/) |
| Tue | Study Amazon SNS architectures, topic definitions, and protocols (Email, SMS, HTTP). | 02/06/2026 | 02/06/2026 | <https://docs.aws.amazon.com/sns/> |
| Wed | Create an SNS Topic, register an email subscriber, and confirm the subscription invitation. | 03/06/2026 | 03/06/2026 | <https://docs.aws.amazon.com/sns/> |
| Thu | Code failure alerts: invoke SNS publish API from Lambda if HTTP codes return non-200. | 04/06/2026 | 04/06/2026 | <https://docs.aws.amazon.com/sns/> |
| Fri | Conduct failure simulation tests, checking for email delivery delays when pinging broken hosts. | 05/06/2026 | 05/06/2026 |  |

### Week 7 Achievements:

* Completed translation for Blog 5.
* Configured a functional, low-latency email warning system using Amazon SNS.
