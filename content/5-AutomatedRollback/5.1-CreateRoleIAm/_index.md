---
title : "Create IAM Role"
date: 2025-07-22
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

### Create **IAM Role** for GitHub Actions:
- In the **IAM** console, click **Roles** from the left sidebar.  
- Click **Create Role** to start the setup.

![5](/images/imageAWS/52.png)

### Step 1: **Select trusted entity**
- Under **Trusted entity type**, choose **Web identity**.
- In **Web identity**, click **Create new** to add GitHub as a provider.

![5](/images/imageAWS/53.png)

### In the **Add Identity Provider** interface:
- Under **Provider details**, first select **OpenID Connect** from the **Provider type** dropdown.
- For **Provider URL**, enter `https://token.actions.githubusercontent.com`.
- For **Audience**, enter `sts.amazonaws.com`.
- Click **Add Provider**.

![5](/images/imageAWS/54.png)

### Go back to the **Step 1** interface:
- Select the newly created provider **token.actions.githubusercontent.com**.

![5](/images/imageAWS/55.png)

- After selecting the provider, fill in the following fields:
  + **Identity**: `token.actions.githubusercontent.com`  
  + **Audience**: `sts.amazonaws.com`  
  + Fill `*` for the last two fields.  
  + Scroll down and click **Next**.

![5](/images/imageAWS/56.png)

### Step 2: Add Permissions
- In the **Permissions policies** section, search for and attach the following permissions:
  - `AmazonRDSFullAccess`
  - `AmazonSSMFullAccess`
  - `CloudWatchLogsFullAccess`
  - `AmazonSNSFullAccess`
- Once all permissions are added, click **Next** to proceed to the final step.
- Example:

![5](/images/imageAWS/57.png)

### Step 3: Name, review, and create
- In **Role name**, enter `github-actions-deploy-role`.
- In **Description**, enter `IAM role for GitHub Actions OIDC access to deploy infrastructure`.

![5](/images/imageAWS/58.png)

- Double-check that all required permissions are attached and no mistakes are present, then click **Create Role**.

![5](/images/imageAWS/59.png)

- The IAM Role has been successfully created:

![5](/images/imageAWS/510.png)
