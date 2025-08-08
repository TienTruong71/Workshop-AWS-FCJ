---
title : "Import services created to Terraform"
date: 2025-07-22
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

In the previous preparation steps, we have created most of the **AWS** services. Now, we will proceed to import and deploy all of them using **Terraform** code snippets.

## Open the **Visual Studio** interface

![3](/images/imageAWS/iac1.png)

- Enter the sample **source** code to lay the foundation for initializing **Terraform**  
```
resource "aws_vpc" "main" {}

provider "aws" {
region = "us-east-1"
}
```

- Then initialize **Terraform** in the **CMD** interface  
```
terraform init
```

- The successful initialization interface will look like the example below  

![3](/images/imageAWS/iac2.png)

## Proceed to import the manually created services  

- In the **CMD** interface, enter:  
```bash
terraform import aws_vpc.main vpc-xxx
```

{{% notice note %}}  
**xxx** is the ID of the service you created, for example, my service here is vpc-00cbeef2469c6bbb  
{{% /notice %}}

![3](/images/imageAWS/iac3.png)

- To synchronize, we need to enter the **source** that matches the imported information. In the **CMD** interface, enter:  
```bash
terraform show
```  

- Immediately, the interface will display information about the created services  

![3](/images/imageAWS/iac4.png)

- We will filter out the important and necessary service attributes to write into the **source**, for example:  

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

- Write the **source** into the code editor in Visual Studio  

![3](/images/imageAWS/iac5.png)

{{% notice tip %}}  
So we have successfully **imported** the VPC service. Similarly, we will **import** the remaining services.  
{{% /notice %}}

- Similarly, **import** the following services one by one, exactly as we did earlier:  

```bash
terraform import aws_subnet.private subnet-xxx

terraform import aws_subnet.public subnet-xxx

terraform import aws_route_table.rt rtb-xxx

terraform import aws_internet_gateway.gw igw-xxx

terraform import aws_security_group.db_sg sg-xxx

terraform import aws_instance.i i-xxx
```

- After completing all **imports**, we will have the following resulting **source**:  

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

- In the final step, we will run the **plan** command to check if there are any **unintended changes**. If the message shows **No changes...** or something similar to the image below, it means the process is successful.  

![3](/images/imageAWS/iac6.png)

#### End of part 3. Next, we will proceed to part 4: **Database** configuration management.
