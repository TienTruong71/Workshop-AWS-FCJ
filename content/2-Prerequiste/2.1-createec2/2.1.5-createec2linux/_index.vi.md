---
title : "Tạo Public Linux EC2"
date: 2025-07-22
weight : 5
chapter : false
pre : " <b> 2.1.5 </b> "
---

1. Truy cập [giao diện quản trị dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)
  + Click **Instances**.
  + Click **Launch instances**.
  
![EC2](/images/2.prerequisite/027-createec2.png)

2. Click vào icon chỉnh sửa nằm dưới cột **Name**
  + Tại hộp thoại **Edit Name**, nhập **IaC Ec2**

![EC2](/images/imageAWS/ec22.png)

3. kéo con trỏ chuột xuống hộp thoại **Instance type** tích chọn **t2.micro** bởi vì đây là phiên bản đủ điều kiện miễn phí 

![EC2](/images/imageAWS/ec23.png)

4. Tại hộp thoại **Select an existing key pair or create a new key pair**.
  + Click chọn **Create a new key pair**.
  + Tại mục **Key pair name** , nhập **IaC**.
  + Tại mục **Key pair type** click chọn loại **RSA**
  + Tại mục **Private key file format** chọn **.pem**
  + Click **Create key pair** và lưu nó lại trong máy tính của bạn.

![EC2](/images/imageAWS/ec24.png)
 
 5. Tại hộp thoại **Network settings**
  + Tại mục **VPC** ,chọn **IaC Workshop**.
  + Tại mục **Subnet**, chọn **IaC Public Subnet**.
  + Tại mục **Auto-assign Public Ip**, chọn **Enable**
  + Tại mục **Firewall (security groups)** lựa chọn security group đã tồn tại
  + Ở bước cuối tại mục**Common security groups** chọn **SG public EC2**
  + Kiểm tra một lần nữa và click **Launch Instance** để chạy EC2 

![EC2](/images/imageAWS/ec25.png)

6. Giao diện khởi tạo thành công

![EC2](/images/imageAWS/ec27.png)


Tiếp theo chúng ta sẽ thực hiện tương tự để tạo 1 EC2 Instance Windows chạy trong Private subnet.