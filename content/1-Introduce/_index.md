---
title : "Introduction"
date: 2025-07-22
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
### Workshop Objectives
This workshop aims to guide learners on how to deploy and manage database infrastructure using **Infrastructure as Code (IaC)** combined with **Configuration Management**, ensuring:
- Automation of database system creation, configuration, and deployment.
- Versioning, rollback, and configuration change control for databases.
- Applicability to various database management systems such as MySQL, PostgreSQL.
- Practice with CI/CD deployment, compliance checks, and resource cleanup after use.

{{%notice tip%}}
**✅ Expected Outcomes**: After the workshop, learners will be able to design database infrastructure with IaC, manage database configuration effectively, and apply it in real-world environments (prod/dev/test).
{{% /notice %}}

### Overview of Infrastructure as Code & Database Configuration Management
- **Infrastructure as Code (IaC)** is a method of managing and provisioning infrastructure through code files instead of manual configuration. For example: Using **Terraform** to create RDS, EC2, VPC, IAM on AWS.  
**Benefits:**
  - Fast and standardized deployment
  - Version control (versioning)
  - Easy to audit, reuse, and rollback
- **Database Configuration Management** is the process of managing database configuration, including:
  - Managing schema, users, permissions
  - Configuring replication, backup, performance tuning
  - Automating setup when deploying databases
  {{%notice note%}}
By combining IaC + Database Configuration Management, you achieve DevOps for databases: easy deployment, rollback, audit, and compliance.
  {{%/notice%}}

### Overall Architecture and Technologies Used
- **Deployment model includes:**
    - IaC (Terraform) to create VPC, Subnet, Security Group, RDS, EC2
    - EC2 connects via AWS SSM or Ansible for database configuration
    - Using GitHub for version control, CI/CD for automation
    - Snapshots and backups for rollback and compliance
- **Technologies Used**

| Component                      | Description                                      |
|---------------------------------|--------------------------------------------------|
| **Terraform**                   | Infrastructure as code deployment                |
| **AWS RDS (MySQL/PostgreSQL)**  | Managed database service                         |
| **AWS Systems Manager (SSM)**   | Secure EC2 connection and configuration          |
| **GitHub & GitHub Actions**     | Source control and deployment automation         |
| **AWS CLI**                     | AWS interaction via command line                 |
| **Ansible (optional)**          | Automated server and database configuration      |