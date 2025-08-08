---
title : "Create Public instance"
date: 2025-07-22
weight : 5
chapter : false
pre : " <b> 2.1.5 </b> "
---

1. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)
  + Click **Instances**.
  + Click **Launch instances**.
  
![EC2](/images/imageAWS/ec21.png)

2. Click the edit icon under the **Name** column
  + In the **Edit Name** dialog box, enter **IaC Ec2**

![EC2](/images/imageAWS/ec22.png)

3. Scroll down on the **Instance type** box then choose instance type is **t2.micro** cause this version is free tier eligible

![EC2](/images/imageAWS/ec23.png)

4. In the **Select an existing key pair or create a new key pair** dialog box.
  + Click to select **Create a new key pair**.
  + In the **Key pair name** field, enter **IaC**.
  + In the **Key pair type** click type **RSA**
  + In the choose box **Private key file format** choose **.pem**
  + Click **Create key pair** and save it to your computer.

![EC2](/images/imageAWS/ec24.png)
 
 5. At **Network settings** dialog box
  + In the **VPC** section, select **IaC Workshop**.
  + In the **Subnet** section, select **IaC Public Subnet**.
  + In the **Auto-assign Public Ip** section, select **Enable**
  + In the **Firewall (security groups)** select existing security group
  + At the end in the **Common security groups** select **SG public EC2**
  + Check again one more time and click **Launch Instance** to run EC2 

![EC2](/images/imageAWS/ec25.png)

6. Successful creation interface

![EC2](/images/imageAWS/ec27.png)


Next, we will do the same to create an EC2 Instance Windows running in the Private subnet.