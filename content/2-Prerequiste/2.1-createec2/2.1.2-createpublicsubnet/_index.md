---
title : "Create Public Subnet"
date: 2025-07-22
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

#### Create Public Subnet

1. Click **Subnets**.
  + Click **Create subnet**.

![VPC](/images/imageAWS/publicsubnet1.png)

2. At the **Create subnet** page.
  + In the **VPC ID** section, click **IaC Workshop**.
  + In the **Subnet name** field, enter **IaC Public Subnet**.
  + In the **AvailabCility Zone** section, select the first Availability zone.
  + In the field **IPv4 CIRD block** enter **10.10.1.0/24**.

![VPC](/images/imageAWS/publicsubnet2.png)

3. Scroll to the bottom of the page, click **Create subnet**.

4. Click **IaC Public Subnet**.
  + Click **Actions**.
  + Click **Edit subnet settings**.

![VPC](/images/imageAWS/publicsubnet3.png)

5. Click **Enable auto-assign public IPv4 address**.
  + Click **Save**.

![VPC](/images/imageAWS/publicsubnet4.png)

6. Click **Internet Gateways**.
  + Click **Create internet gateway**.
  
![VPC](/images/imageAWS/publicsubnet5.png)

7. At the **Create internet gateway** page.
  + In the **Name tag** field, enter **IaC IGW**.
  + Click **Create internet gateway**.
  
![VPC](/images/imageAWS/publicsubnet6.png)

8. After successful creation, click **Actions**.
  + Click **Attach to VPC**.
 
![VPC](/images/imageAWS/publicsubnet7.png)

9. At the **Attach to VPC** page.
  + In the **AvaiIaCle VPCs** section, select **IaC VPC**.
  + Click **Attach internet gateway**.
  + Check the successful attaching process as shown below.

![VPC](/images/imageAWS/publicsubnet8.png)

10. Next we will create a custom route table to assign to **IaC Public Subnet**.
  + Click **Route Tables**.
  + Click **Create route table**.

![VPC](/images/imageAWS/publicsubnet9.png)

11. At the **Create route table** page.
  + In the **Name** field, enter **IaC Publicrtb**.
  + In the **VPC** section, select **IaC VPC**.
  + Click **Create route table**.

![VPC](/images/imageAWS/publicsubnet10.png)

12. After creating the route table successfully.
  + Click **Edit routes**.
  
![VPC](/images/imageAWS/publicsubnet11.png)

13. At the **Edit routes** page.
  + Click **Add route**.
  + In the **Destination** field, enter 0.0.0.0/0
  + In the **Target** section, select **Internet Gateway** and then select **IaC IGW**.
  + Click **Save changes**.

![VPC](/images/imageAWS/publicsubnet12.png)

14. Click the **Subnet associations** tab.
  + Click **Edit subnet associations** to proceed with the associate custom route table we just created in **IaC Public Subnet**.


![VPC](/images/imageAWS/publicsubnet13.png)

15. At the **Edit subnet associations** page.
  + Click on **IaC Public Subnet**.
  + Click **Save associations**.

![VPC](/images/imageAWS/publicsubnet14.png)

16. Check that the route table information has been associated with **IaC Public Subnet** and the internet route information has been pointed to the Internet Gateway as shown below.

![VPC](/images/imageAWS/publicsubnet15.png)
