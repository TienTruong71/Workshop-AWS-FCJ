---
title : "Lưu trữ cấu hình trong parameter store bằng terraformm "
date: 2025-07-22
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---


Trong bước này, chúng ta sẽ tạo lần lượt các file có đuôi **.tf** để thực hiện những mục đích sau:

| File                 | Mục đích                                                       |
| -------------------- | -------------------------------------------------------------- |
| `variables.tf`       | Khai báo các biến cấu hình như DB name, username, subnet, v.v. |
| `terraform.tfvars`   | Truyền giá trị cụ thể cho các biến đã khai báo                  |
| `rds.tf`             | Tạo RDS MySQL và subnet group                                  |
| `parameter_store.tf` | Lưu thông tin RDS (endpoint, user, pass) vào Parameter Store   |
| `outputs.tf`         | Xuất thông tin sau khi apply để kiểm tra nhanh                 |

  - Khởi tạo các **file** theo cấu trúc bên dưới:

![4](/images/imageAWS/511.png)

### Truyền giá trị tương ứng cho từng **file**, cụ thể:

#### **Variables.tf**

```
variable "db_name" {
description = "IaC DTB"
type        = string
default     = "myappdb"
}

variable "db_username" {
description = "tientruong"
type        = string
default     = "admin"
}

variable "db_password" {
description = "Tien2004"
type        = string
sensitive   = true
}

variable "db_instance_class" {
description = "db.t3.micro"
type        = string
default     = "db.t3.micro"
}

variable "vpc_id" {
description = "vpc-00cbeef2469c6bbb4"
type        = string
}

variable "subnet_ids" {
description = "List of subnet IDs to launch RDS instance"
type        = list(string)
}
```

#### **rds.tf**

```
resource "aws_db_subnet_group" "rds_subnet" {
name       = "rds-subnet-group"
subnet_ids = var.subnet_ids
tags = {
Name = "RDS subnet group"
}
}

resource "aws_db_instance" "mysql" {
identifier         = "workshop-mysql"
engine             = "mysql"
engine_version     = "8.0"
instance_class     = var.db_instance_class
allocated_storage  = 20
storage_type       = "gp2"
db_name               = var.db_name
username           = var.db_username
password           = var.db_password
publicly_accessible = false
db_subnet_group_name = aws_db_subnet_group.rds_subnet.name
vpc_security_group_ids = ["sg-0d39988e861c6e057"]

skip_final_snapshot = true
deletion_protection = false

tags = {
Name = "RDS MySQL"
}
}

```
#### **parameter_store.tf**
``` 
resource "aws_ssm_parameter" "db_endpoint" {
name  = "/workshop/db/endpoint"
type  = "String"
value = aws_db_instance.mysql.endpoint
}

resource "aws_ssm_parameter" "db_username" {
name  = "/workshop/db/username"
type  = "String"
value = var.db_username
}

resource "aws_ssm_parameter" "db_password" {
name   = "/workshop/db/password"
type   = "SecureString"
value  = var.db_password
}
```

#### **outputs.tf**

```
output "rds_endpoint" {
value = aws_db_instance.mysql.endpoint
}

output "rds_db_name" {
value = aws_db_instance.mysql.name
}

```
#### **terraform.tfvars**

```
db_password = "Tien2004"
vpc_id      = "vpc-00cbeef2469c6bbb4"
subnet_ids  = ["subnet-0f09c08ad471977c7", "subnet-05ed4b65e35cf79b8"]

sau đó nhập lần lượt các dòng lệnh sau 

terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars"
```
  - Sau khi tạo và truyền giá trị đủ các **file**, chạy lần lượt các lệnh sau trong **CMD**:
  ```bash
  terraform init 
  ``` 

![4](/images/imageAWS/42.png)

```bash
terraform plan -var-file="terraform.tfvars
```
![4](/images/imageAWS/43.png)

```bash
terraform plan -var-file="terraform.tfvars
```
![4](/images/imageAWS/45.png)

{{%notice warning%}}
Trên giao diện hiển thị bảng thông báo, bạn chỉ cần nhập **"yes"**
{{% /notice %}}
- Đợi khoảng **5 phút** để khởi tạo

![4](/images/imageAWS/46.png)

Vậy khép lại phần 4, ta tiếp tục đến **phần 5 triển khai tự động và rollback**