---
title : "Quản lý cấu hình Database"
date: 2025-07-22 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---


Trong phần này, chúng ta sẽ tập trung vào **việc quản lý và cấu hình cơ sở dữ liệu** đã được triển khai thông qua Infrastructure as Code (IaC).  
Sau khi hoàn tất việc triển khai hạ tầng và thiết lập kết nối giữa các máy chủ EC2 public và private, bước tiếp theo là cấu hình môi trường cơ sở dữ liệu để đáp ứng yêu cầu của ứng dụng.

Nội dung sẽ bao gồm:
- Cài đặt và cấu hình phần mềm cơ sở dữ liệu.
- Áp dụng cấu trúc dữ liệu ban đầu hoặc dữ liệu mẫu.
- Điều chỉnh các thiết lập bảo mật và hiệu năng.
- Kiểm tra khả năng kết nối giữa các thành phần ứng dụng và cơ sở dữ liệu.

Kết thúc phần này, bạn sẽ có một môi trường cơ sở dữ liệu đã được cấu hình đầy đủ, sẵn sàng cho triển khai trong môi trường giả lập sản xuất.


### Nội dung:

  - [Cập nhật IAM Role](./4.1-updateiamrole/)
  - [Tạo **S3 Bucket**](./4.2-creates3bucket/)
  - [Tạo S3 Gateway endpoint](./4.3-creategwes3)
  - [Cấu hình **Session logs**](./4.4-configsessionlogs/)
