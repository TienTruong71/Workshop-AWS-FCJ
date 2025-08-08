---
title : "Phát triển hạ tầng IaC cho Database"
date: 2025-07-22 
weight : 3 
chapter : true
pre : " <b> 3. </b> "
---

Trong hai phần trước, chúng ta đã chuẩn bị đầy đủ môi trường làm việc, cài đặt **Terraform**, khởi tạo dự án và triển khai các thành phần cơ bản của hạ tầng như **VPC**, **subnet**, **security group**, cùng với việc cấu hình kết nối **GitHub** để quản lý mã nguồn.  

Bước sang **Phần 3**, mục tiêu của chúng ta là **mở rộng hạ tầng IaC để phục vụ cho cơ sở dữ liệu**, bao gồm triển khai và cấu hình các máy chủ **EC2** (cả *public* và *private*) đóng vai trò trung gian hoặc trực tiếp kết nối tới **Database**.

## Nội dung chính

- Thiết lập kết nối tới **EC2 Public** để quản lý và kiểm tra hệ thống.  
- Cấu hình kết nối an toàn tới **EC2 Private** thông qua các dịch vụ AWS như **VPC Endpoint** và **Systems Manager**.  
- Đảm bảo việc truy cập **Database** được thực hiện một cách **an toàn, có kiểm soát** và phù hợp với mô hình mạng đã thiết kế ở các phần trước.  

---
 **Kết quả đạt được sau phần này:**  
Bạn sẽ có một hệ thống hạ tầng **đầy đủ lớp kết nối** từ ngoài Internet vào tới các dịch vụ bên trong *Private subnet*, sẵn sàng cho bước quản lý và vận hành Database ở phần tiếp theo.


### Nội dung
3.1. [Nhập các dịch vụ đã tạo cho Terraform](3.1-import-services/) 
