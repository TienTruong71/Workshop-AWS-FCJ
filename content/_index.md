---
title : "Session Management"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Database Configuration Management & Infrastructure as Code (IaC)

### Overview

This workshop aims to guide learners on how to deploy and manage database infrastructure using Infrastructure as Code (IaC), combined with Configuration Management, to ensure:
- Automation of the process of creating, configuring, and deploying database systems.
- Versioning, rollback capabilities, and configuration change control for databases.
- Applicability to various database management systems such as MySQL and PostgreSQL.
- Hands-on practice with CI/CD deployment, compliance checks, and resource cleanup after use.

{{% notice success %}}
Expected outcomes: After the workshop, students should be able to independently design database infrastructure using IaC, effectively manage database configurations, and apply this knowledge in real-world environments (prod/dev/test).
{{% /notice %}}

![ConnectPrivate](/images/arc-log.png) 

### Nội dung

 1. [Introduction](1-introduce/)
 2. [Preparation](2-Prerequiste/)
 3. [Developing IaC Infractructure for Databases](3-Accessibilitytoinstance/)
 4. [Database Configuration Management](4-s3log/)
 5. [Automated Deployment and Rollback](5-Portfwd/)
 6. [Compliance & Change Control](6-cleanup/)
 7. [Clean up resource](7-test/)
