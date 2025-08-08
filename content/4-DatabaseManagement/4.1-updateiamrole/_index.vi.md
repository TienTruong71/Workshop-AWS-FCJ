---
title : "Tạo Private Subnet"
date: 2025-07-22 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

Ở bước chuẩn bị trước chúng ta mới chỉ có 1 **Private Subnet** nhưng khi tạo RDS ta cần 2. Vì vậy cần tạo thêm 1 **Private Subnet**
1. Ở trang giao diện VPC
. Click **Subnets**.
  + Click **Create subnet**.

2. Tại trang **Create subnet**.
  + Tại mục **VPC ID** click chọn **IaC Workshop**.
  + Tại mục **Subnet name** điền **RDS Private Subnet**.
  + Tại mục **Availability Zone** chọn Availability zone thứ 2.
  + Tại mục **IPv4 CIRD block** điền **10.10.3.0/24**.

![VPC](/images/imageAWS/41.png)

4. Kéo xuống cuối trang , click **Create subnet**.