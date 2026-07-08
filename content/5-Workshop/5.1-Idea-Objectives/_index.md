---
title: "Idea & Objectives"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---


### 1. Context & Problem Statement
Organizations and developers require real-time uptime monitoring to prevent prolonged website outages. A typical solution requires constant infrastructure uptime, which runs into cost and maintenance overheads. This project provides an automated, serverless, ultra-low-cost (virtually free) monitoring solution that immediately pushes notifications when problems arise.

*   **Target Audience:** System Administrators (SysAdmin), DevOps teams, and website owners.
*   **Proposed Solution:** A serverless scheduler pinging target websites every 5 minutes, storing response latency records for historical analysis, and pushing instant email alerts on HTTP failures.

### 2. Success Criteria
*   **Infrastructure as Code:** Complete deployment automated with Terraform.
*   **Data Archival:** Persistent logs written to a NoSQL database.
*   **Alert Latency:** Email notification sent within 1 minute of detecting an outage.
