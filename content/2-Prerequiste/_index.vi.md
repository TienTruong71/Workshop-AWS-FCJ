---
title : "Các bước chuẩn bị"
date: 2025-07-22
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Để triển khai thành công các thực hành về **Infrastructure as Code (IaC)** và **Quản lý cấu hình cơ sở dữ liệu (Database Configuration Management)** trên AWS, việc thiết lập một môi trường hạ tầng chuẩn là vô cùng quan trọng. Phần này trình bày các bước cần thiết để xây dựng hạ tầng, cài đặt công cụ và đảm bảo môi trường làm việc mô phỏng sát thực tế sản xuất, bao gồm cả subnet công khai và subnet riêng.

{{% notice info %}}
Trong phần này, chúng ta tiến hành tạo lập các thành phần hạ tầng mạng và máy ảo (EC2) nhằm mô phỏng một hệ thống thật. Cấu trúc bao gồm: cấu hình VPC, các subnet, cổng Internet, bảng định tuyến và khởi tạo các EC2 instance để cài đặt các công cụ quản lý cấu hình và cơ sở dữ liệu.
{{% /notice %}}

Để tìm hiểu cách tạo các EC2 instance và VPC với public/private subnet các bạn có thể tham khảo bài lab :
  - [Giới thiệu về Amazon EC2](https://000004.awsstudygroup.com/vi/)
  - [Làm việc với Amazon VPC](https://000003.awsstudygroup.com/vi/)

Việc chuẩn bị môi trường bao gồm nhiều khía cạnh như xây dựng **kiến trúc mạng (VPC)**, tạo subnet công khai và subnet riêng, thiết lập các nhóm bảo mật, và khởi tạo các máy chủ **EC2 (Linux và Windows)** để triển khai các công cụ và ứng dụng. Ngoài ra, còn phải cài đặt các công cụ thiết yếu như **Terraform, AWS CLI, Git, Visual Studio Code** và cấu hình **AWS Systems Manager** để phục vụ cho việc truy cập và quản trị máy chủ từ xa một cách bảo mật.

### Nội dung
  - [Chuẩn bị VPC và EC2 Instance](2.1-createec2/)
  - [Cài đặt các công cụ cần thiết](2.2-installTools/)

  
