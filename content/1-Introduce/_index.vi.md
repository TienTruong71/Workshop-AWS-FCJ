---
title : "Giới thiệu"
date: 2025-07-22
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
### Mục tiêu Workshop 
Workshop này nhằm hướng dẫn người học cách triển khai và quản lý hạ tầng cơ sở dữ liệu bằng phương pháp **Infrastructure as Code (IaC)** , kết hợp với **Configuration Management**, đảm bảo:
- Tự động hóa quá trình tạo, cấu hình và triển khai hệ thống database.
- Đảm bảo khả năng version hóa, rollback, và kiểm soát thay đổi cấu hình CSDL.
- Áp dụng được cho nhiều loại hệ quản trị cơ sở dữ liệu như MySQL, PostgreSQL.
- Thực hành triển khai CI/CD, kiểm tra tuân thủ và dọn dẹp tài nguyên sau khi sử dụng.

{{%notice tip%}}
**✅ Kết quả mong đợi**: Học viên sau workshop có thể tự thiết kế hạ tầng database bằng IaC, quản lý cấu hình database hiệu quả, và áp dụng vào môi trường thực tế (prod/dev/test).
{{% /notice %}}


### Tổng quan về Infrastructure as Code & Database Configuration Management
- **Infrastructure as Code (IaC)** là phương pháp quản lý và cung cấp hạ tầng thông qua tập tin mã hóa thay vì cấu hình thủ công. ví dụ: Dùng **Terrafrom** để tạo RDS, EC2, VPC, IAM trên AWS. 
**Lợi ích:**
    - Triển khai nhanh và chuẩn hóa 
    - Có thể kiểm soát phiên bản (versioning)
    - Dễ kiểm tra, tái sử dụng, rollback 
- **Database Configuration Management** là quá trình quản lý cấu hình của cơ sở dữ liệu, bao gồm:
    - Quản lý schema, user, permission
    - Cấu hình replication, backup, performance tuning
    - Tự động hóa tạo các thiết lập khi deploy DB
    {{%notice note%}}
Khi kết hợp IaC + Database Configuration Management, ta đạt được DevOps cho database: dễ deploy, rollback, audit, và đảm bảo compliance. 
    {{%/notice%}}


### Kiến trúc tổng thể và công nghệ sử dụng 
- **Mô hình triển khai bao gồm**
    - IaC (Terraform) tạo VPC, Subnet, Security Group, RDS, EC2
    - EC2 kết nối qua AWS SSM hoặc Ansible để cấu hình database
    - Sử dụng GitHub để version hóa, CI/CD để tự động hóa
    - Snapshot và backup phục vụ rollback và compliance
- **Công nghệ sử dụng**

| Thành phần                | Mô tả                                         |
|--------------------------|------------------------------------------------|           
| **Terraform**            | Triển khai hạ tầng dưới dạng code             |            
| **AWS RDS (MySQL/PostgreSQL)** | Dịch vụ cơ sở dữ liệu có quản lý         |              
| **AWS Systems Manager (SSM)**  | Kết nối và cấu hình máy chủ EC2 an toàn  |               
| **GitHub & GitHub Actions**    | Quản lý mã nguồn và tự động hóa triển khai |                
| **AWS CLI**              | Tương tác với AWS thông qua dòng lệnh         |                    
| **Ansible (tùy chọn)**   | Cấu hình máy chủ và database tự động          |  
                  