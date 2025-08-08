---
title : "Database Configuration Management"
date: 2025-07-22
weight : 4
chapter : false
pre : " <b> 4. </b> "
---


# Part 4 – Database Configuration Management

In this section, we will focus on **managing and configuring the database** that we have provisioned using Infrastructure as Code (IaC).  
After successfully deploying our infrastructure and establishing connectivity between the public and private EC2 instances, the next step is to configure the database environment to meet application requirements.

We will cover tasks such as:
- Installing and configuring the database software.
- Applying initial schema or seed data.
- Adjusting security and performance settings.
- Verifying connectivity between application components and the database.

By the end of this part, you will have a fully configured and operational database environment, ready for deployment in a production-like setting.

### Content:

   - [Create Public Subnet](./4.1-updateiamrole/)
   - [Create **S3 Bucket**](./4.2-creates3bucket/)
   - [Create S3 Gateway endpoint](./4.3-creategwes3)
   - [Configure **Session logs**](./4.4-configsessionlogs/)