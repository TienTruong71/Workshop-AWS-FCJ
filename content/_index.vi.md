---
title : "Session Management"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Quản lý cấu hình cơ sở dữ liệu & hạ tầng dưới dạng mã (IaC)

### Tổng quan

Workshop này nhằm hướng dẫn người học cách triển khai và quản lý hạ tầng cơ sở dữ liệu bằng phương pháp **Infrastructure as Code (IaC)**, kết hợp với **Configuration Management**, đảm bảo:
- Tự động hóa quá trình tạo, cấu hình và triển khai hệ thống database.
- Đảm bảo khả năng version hóa, rollback, và kiểm soát thay đổi cấu hình CSDL.
- Áp dụng được cho nhiều loại hệ quản trị cơ sở dữ liệu như MySQL, PostgreSQL.
- Thực hành triển khai CI/CD, kiểm tra tuân thủ và dọn dẹp tài nguyên sau khi sử dụng.

{{% notice note %}}
Kết quả mong đợi: Học viên sau workshop có thể tự thiết kế hạ tầng database bằng IaC, quản lý cấu hình database hiệu quả, và áp dụng vào môi trường thực tế (prod/dev/test).
{{% /notice %}}

![ConnectPrivate](/images/arc-log.png) 

### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-Prerequiste/)
 3. [Phát triển hạ tầng IaC cho Database](3-Accessibilitytoinstance/)
 4. [Quản lý cấu hình Database](4-s3log/)
 5. [Triển khai tự động và Rollback](5-Portfwd/)
 6. [Đảm bảo tuân thủ & kiểm soát thay đổi](6-cleanup/)
 7. [Dọn dẹp tài nguyên](7-test/)
