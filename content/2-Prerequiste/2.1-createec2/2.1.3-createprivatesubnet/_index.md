---
title : "Create Private Subnet"
date: 2025-07-22
weight : 3
chapter : false
pre : " <b> 2.1.3 </b> "
---

#### Create Private Subnet

1. Click **Subnets**.
   + Click **Create subnet**.

![VPC](/images/imageAWS/privatesubnet1.png)

2. At the **Create subnet** page.
   + In the **VPC ID** section, click **IaC VPC**.
   + In the **Subnet name** field, enter **IaC Private Subnet**.
   + In the **Availability Zone** section, select the first Availability zone.
   + In the field **IPv4 CIRD block** enter **10.10.2.0/24**.

![VPC](/images/imageAWS/privatesubnet2.png)

3. successful creation interface

![VPC](/images/imageAWS/privatesubnet3.png)


4. Scroll to the bottom of the page, click **Create subnet**.

The next step is to create the necessary security groups for the lab.