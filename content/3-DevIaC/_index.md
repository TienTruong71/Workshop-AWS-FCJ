---
title : "Developing IaC Infrastructure for Database"
date: 2025-07-22
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

In the previous sections, we prepared the working environment, installed **Terraform**, initialized the project, and deployed the core infrastructure components such as **VPC**, **subnets**, **security groups**, along with configuring **GitHub** for source code management.  

Moving into **Part 3**, our goal is to **extend the IaC infrastructure to support the database**, including deploying and configuring **EC2 instances** (both *public* and *private*) that act as intermediaries or directly connect to the **Database**.

## Key Objectives

- Set up connections to **Public EC2** instances for system management and verification.  
- Configure secure access to **Private EC2** instances using AWS services like **VPC Endpoint** and **Systems Manager**.  
- Ensure database access is performed **securely, with controlled permissions**, and follows the network architecture designed in the previous sections.  

---
 **Outcome after this section:**  
You will have a complete **end-to-end connectivity layer** from the public internet to services inside the *Private subnet*, ready for database management and operations in the next stage.

### Content
3.1. [Import Service created to Terraform](3.1-import-services/) 
