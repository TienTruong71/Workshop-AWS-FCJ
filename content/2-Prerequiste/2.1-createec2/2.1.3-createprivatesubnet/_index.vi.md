---
title : "Tạo Private subnet"
date: 2025-07-22
weight : 3
chapter : false
pre : " <b> 2.1.3 </b> "
---

#### Tạo Private subnet

1. Click **Subnets**.
  + Click **Create subnet**.

![VPC](/images/imageAWS/privatesubnet1.png)

2. Tại trang **Create subnet**.
  + Tại mục **VPC ID** click chọn **IaC VPC**.
  + Tại mục **Subnet name** điền **IaC Private Subnet**.
  + Tại mục **Availability Zone** chọn Availability zone đầu tiên.
  + Tại mục **IPv4 CIRD block** điền **10.10.2.0/24**.

![VPC](/images/imageAWS/privatesubnet2.png)
3. Giao diện khởi tạo thành công

![VPC](/images/imageAWS/privatesubnet3.png)

4. Kéo xuống cuối trang , click **Create subnet**.

Bước tiếp theo chúng ta sẽ tạo các security group cần thiết cho bài lab.