---
title : "Update IAM Role"
date: 2025-07-22
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

In the previous preparation step, we only had **one Private Subnet**, but when creating an RDS instance, we need two. Therefore, we must create an additional **Private Subnet**.

1. On the **VPC** console page:  
   - Click **Subnets**.  
   - Click **Create subnet**.  

2. On the **Create subnet** page:  
   - In the **VPC ID** field, select **IaC Workshop**.  
   - In the **Subnet name** field, enter **RDS Private Subnet**.  
   - In the **Availability Zone** field, select the second Availability Zone.  
   - In the **IPv4 CIDR block** field, enter **10.10.3.0/24**.  

![VPC](/images/imageAWS/41.png)

3. Scroll to the bottom of the page and click **Create subnet**.
