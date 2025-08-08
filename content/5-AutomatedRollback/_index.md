---
title : "Automated Deployment & Rollback"
date: 2025-07-22
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

In this section, we will set up an **automated application deployment process** (CI/CD) along with a **rollback mechanism** in case of failures.  
The goal is to ensure that every source code change pushed to the repository is deployed quickly, safely, and can be reverted to a stable previous version if any issues arise.

### Objectives
- Configure a pipeline to automatically build, test, and deploy the application.
- Set up a deployment trigger when a new commit is pushed to the **main branch**.
- Apply a rollback strategy to minimize downtime in case of a failed deployment.
- Test the rollback process to ensure recovery capability.

### Expected Outcomes
By the end of this section, you will understand:
1. The full **automated deployment process** from commit to the production environment.
2. How to integrate a **rollback mechanism** to safeguard the system during new releases.
3. How to perform a safe and fast rollback in practice.

### Content:

- [Create IAM Role](./5.1-CreateRoleIAm/)
- [Automated Deployment & Rollback](./5.2-AutoRollback/)
