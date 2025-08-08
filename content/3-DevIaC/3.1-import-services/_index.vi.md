---
title : "Nhập các dịch vụ đã tạo cho Terraform"
date: 2025-07-22 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

Ở các bước chuẩn bị trước, chúng ta đã tạo hầu hết các dịch vụ của **AWS**, sau đây chúng ta sẽ thực hiện việc nhập và triển khai tất cả bằng những đoạn mã **Terraform**

## Mở giao diện **Visual studio**

![3](/images/imageAWS/iac1.png)

  - Nhập đoạn **source** mẫu tạo nền móng để khởi tạo **Terraform**
```
resource "aws_vpc" "main" {}

provider "aws" {
region = "us-east-1"
}
```
  - Sau đó khởi tạo **Terraform** trong giao diện **CMD**
```
terraform init
```
  - Giao diện khởi tạo thành công như hình mẫu bên dưới

![3](/images/imageAWS/iac2.png)

## Tiến hành Import các dịch vụ đã khởi tạo thủ công 

  - Ở giao diện **CMD** nhập 
  ```bash
  terraform import aws_vpc.main vpc-xxx
  ```

{{% notice note %}}
  **xxx** là id của những dịch vụ đã khởi tạo, ví dụ dịch vụ của mình ở đây là vpc-00cbeef2469c6bbb
{{% /notice %}}

![3](/images/imageAWS/iac3.png)

 - Để đồng bộ, chúng ta cần nhập **source** trùng khớp với những thông tin đã **import**. Cùng trên giao diện **CMD** nhập:
 ```bash
terraform show
 ``` 
  - Ngay lập tức giao diện xuất hiện thông tin những dịch vụ đã khởi tạo  

![3](/images/imageAWS/iac4.png)

  - Chúng ta sẽ chọn lọc những hạng mục của dịch vụ quan trọng và cần thiết để viết vào **Source**, cụ thể như:

```
resource "aws_vpc" "main" {
cidr_block                           = "10.10.0.0/16"
enable_dns_support                   = true
enable_dns_hostnames                 = false
enable_network_address_usage_metrics = false
instance_tenancy                     = "default"

tags = {
Name = "IaC workshop "
}
}
```
  - Viết **Source** vào giao diện code trong visual 

![3](/images/imageAWS/iac5.png)

{{% notice tip %}}
  Vậy là chúng ta đã **import** thành công dịch vụ VPC, tương tự ta sẽ **Import** với những dịch vụ còn lại khác.
{{% /notice %}}

  - Tương tự **Import** lần lượt những dịch vụ sau y như cách lúc nãy ta đã làm  
 
```bash
terraform import aws_subnet.private subnet-xxx

terraform import aws_subnet.public subnet-xxx

terraform import aws_route_table.rt rtb-xxx

terraform import aws_internet_gateway.gw igw-xxx

terraform import aws_security_group.db_sg sg-xxx

terraform import aws_instance.i i-xxx
```

  - sau khi đã **Import** hoàn tất, ta được đoạn **Source** kết quả sau:

```
resource "aws_vpc" "main" {
cidr_block           = "10.10.0.0/16"
enable_dns_support   = true
enable_dns_hostnames = false
instance_tenancy     = "default"

tags = {
Name = "IaC workshop "
}
}

resource "aws_subnet" "public" {
vpc_id                  = aws_vpc.main.id
cidr_block              = "10.10.1.0/24"
availability_zone       = "us-east-1a"
map_public_ip_on_launch = true

tags = {
Name = "IaC Public Subnet "
}
}

resource "aws_subnet" "private" {
vpc_id            = aws_vpc.main.id
cidr_block        = "10.10.2.0/24"
availability_zone = "us-east-1a"

tags = {
Name = "IaC Private Subnet"
}
}

resource "aws_internet_gateway" "gw" {
vpc_id = aws_vpc.main.id

tags = {
Name = "IaC IGW"
}
}

resource "aws_route_table" "rt" {
vpc_id = aws_vpc.main.id

route {
cidr_block = "0.0.0.0/0"
gateway_id = aws_internet_gateway.gw.id
}

tags = {
Name = "IaC publicRTB"
}
}

resource "aws_security_group" "db_sg" {
name        = "SG public EC2"
description = "SG public EC2"
vpc_id      = aws_vpc.main.id

egress {
from_port   = 0
to_port     = 0
protocol    = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
}

resource "aws_security_group" "private" {
name        = "SG private windows Instance"
description = "SG private windows Instance"
vpc_id      = aws_vpc.main.id

egress {
from_port   = 0
to_port     = 0
protocol    = "-1"
cidr_blocks = ["0.0.0.0/0"]
}

egress {
from_port   = 443
to_port     = 443
protocol    = "tcp"
cidr_blocks = ["10.10.0.0/16"]
}
}

resource "aws_security_group" "sgvpcendpoint" {
name        = "SG VPC Endpoint"
description = "SG VPC Endpoint"
vpc_id      = aws_vpc.main.id
}

resource "aws_instance" "i" {
ami                    = "ami-08a6efd148b1f7504"
instance_type          = "t2.micro"
subnet_id              = aws_subnet.public.id
key_name               = "IaC"
associate_public_ip_address = true

vpc_security_group_ids = [
aws_security_group.db_sg.id
]

root_block_device {
volume_type           = "gp3"
volume_size           = 8
iops                  = 3000
throughput            = 125
delete_on_termination = true
device_name           = "/dev/xvda"
}

credit_specification {
cpu_credits = "standard"
}

capacity_reservation_specification {
capacity_reservation_preference = "open"
}

metadata_options {
http_endpoint               = "enabled"
http_tokens                 = "required"
http_put_response_hop_limit = 2
http_protocol_ipv6          = "disabled"
instance_metadata_tags      = "disabled"
}

tags = {
Name = "IaC EC2"
}
}
provider "aws" {
region = "us-east-1"

}
```
  - Ở bước cuối cùng, ta sẽ tiến hành kiểm tra **plan** để xem rằng có sự **thay đổi không chủ đích** nào xảy ra không. Nếu thông báo hiện **No changes...** hoặc tương tự như ảnh bên dưới là đã thành công.
  
![3](/images/imageAWS/iac6.png)


#### Kết thúc phần 3, tiếp theo ta sẽ tiến hành đến phần 4 quản lý cấu hình **Database**