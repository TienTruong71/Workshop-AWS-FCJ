---
title : "Store configuration in Parameter Store using Terraform"
date: 2025-07-22
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

In this step, we will sequentially create `.tf` files to achieve the following purposes:

| File                 | Purpose                                                                 |
| -------------------- | ----------------------------------------------------------------------- |
| `variables.tf`       | Declare configuration variables such as DB name, username, subnet, etc.|
| `terraform.tfvars`   | Assign specific values to the declared variables                        |
| `rds.tf`             | Create an RDS MySQL instance and subnet group                           |
| `parameter_store.tf` | Store RDS information (endpoint, username, password) in Parameter Store |
| `outputs.tf`         | Output information after apply for quick verification                   |

- Initialize the **files** according to the structure below:

![4](/images/imageAWS/511.png)

### Assign the corresponding values for each **file** as follows:

#### **variables.tf**
```
variable "db_name" {
  description = "IaC DB"
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
  identifier              = "workshop-mysql"
  engine                  = "mysql"
  engine_version          = "8.0"
  instance_class          = var.db_instance_class
  allocated_storage       = 20
  storage_type            = "gp2"
  db_name                 = var.db_name
  username                = var.db_username
  password                = var.db_password
  publicly_accessible     = false
  db_subnet_group_name    = aws_db_subnet_group.rds_subnet.name
  vpc_security_group_ids  = ["sg-0d39988e861c6e057"]

  skip_final_snapshot     = true
  deletion_protection     = false

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
```

---

After creating and assigning values to all the **files**, run the following commands in your **terminal**:

```
terraform init
```
![4](/images/imageAWS/42.png)

```
terraform plan -var-file="terraform.tfvars"
```
![4](/images/imageAWS/43.png)

```
terraform apply -var-file="terraform.tfvars"
```
![4](/images/imageAWS/45.png)

{{% notice warning %}}
When prompted, simply type **"yes"** to confirm.
{{% /notice %}}

- Wait about **5 minutes** for the resources to be created.

![4](/images/imageAWS/46.png)

This wraps up **Part 4**, and we can proceed to **Part 5 – Automated Deployment and Rollback**.
