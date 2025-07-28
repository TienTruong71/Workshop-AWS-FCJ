---
title : "Preparation "
date: 2025-07-22
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

To successfully implement **infrastructure as code (IaC)** and **database configuration management** practices in AWS, it is essential to establish a well-defined environment. This section outlines the necessary steps to provision the infrastructure and install the required tools. The setup will ensure a seamless and secure foundation for deploying and managing services across both public and private subnets.

{{% notice info %}}
In this part, we provision a network environment and virtual machines to simulate a real-world production-like system using AWS. The infrastructure includes creating networking components, setting security policies, and launching EC2 instances to host configuration management tools and databases.
{{% /notice %}}

To learn how to create EC2 instances and VPCs with public/private subnets, you can refer to the lab:
  - [About Amazon EC2](https://000004.awsstudygroup.com/en/)
  - [Works with Amazon VPC](https://000003.awsstudygroup.com/en/)

Preparing the environment includes many aspects such as building the **network architecture (VPC)**, creating public and private subnets, setting up security groups, and initializing **EC2 (Linux and Windows)** servers to deploy tools and applications. Additionally, essential tools like **Terraform, AWS CLI, Git, Visual Studio Code** must be installed, and **AWS Systems Manager** must be configured to facilitate secure remote access and management of the servers.

### Content
  - [AWS Infrastructure Setup](2.1-createec2/)
  - [Install Required Tools](2.2-installTools/)