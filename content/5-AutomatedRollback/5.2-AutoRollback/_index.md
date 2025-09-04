---
title : "Automatic Deployment and Rollback"
date: 2025-07-22
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

- In this part 5, we will first create a **GitHub Repository** to store the environment for running CI/CD.

### Create a Repository on GitHub

#### Step 1: Log in to GitHub
1. Go to [https://github.com](https://github.com).
2. Log in with your GitHub account.

---

#### Step 2: Create a New Repository
1. In the top-right corner, click the **`+`** button → choose **"New repository"**.
2. Fill in the details:
   - **Repository name**: Repo name (e.g., `terraform CICD Workshop`).
   - **Description** *(optional)*
   - **Visibility**:
     - `Public`: Anyone can view.
     - `Private`: Only you (and invited members) can view.
   - **Initialize this repository with**:
     - Select **Add a README file** if you want to create `README.md` right away.
     - Select **Add .gitignore** to exclude unnecessary files/folders from pushing.
     - Select **Choose a license** if you want to add a usage license.

![5](/images/imageAWS/51.png)

---

#### Step 3: Finish Creating the Repository
- Click **Create repository**.
- You will be redirected to the newly created repo page.

---

### CI/CD Deployment

#### Create folder structure in **Visual Studio**
- Create a file named `ci-cd.yml` inside the **.github\workflows** folder, similar to the image below.

![5](/images/imageAWS/511.png)

#### Content of **ci-cd.yml**

```
name: Deploy RDS with Snapshot Backup

on:
  push:
    branches:
      - main

permissions:
  id-token: write
  contents: read

jobs:
  deploy:
    name: Terraform Deploy with Snapshot
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          role-to-assume: arn:aws:iam::<account-id>:role/github-terraform-role
          aws-region: ap-southeast-1

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: 1.6.0

      - name: Init Terraform
        run: terraform -chdir=terraform init

      - name: Create Snapshot before Deployment
        run: |
          aws rds create-db-snapshot \
            --db-instance-identifier workshop-mysql \
            --db-snapshot-identifier workshop-mysql-$(date +%Y%m%d%H%M%S)

      - name: Terraform Plan
        run: terraform -chdir=terraform plan -var-file="terraform.tfvars"

      - name: Terraform Apply
        run: terraform -chdir=terraform apply -auto-approve -var-file="terraform.tfvars"

      - name: Notify success
        if: success()
        run: |
          aws sns publish \
            --topic-arn arn:aws:sns:ap-southeast-1:<account-id>:db-deploy-topic \
            --message "RDS deployment completed successfully." \
            --subject "RDS Deployment"

  rollback:



  =========================    
    name: Rollback from last snapshot
    runs-on: ubuntu-latest
    needs: deploy
    if: failure()
    steps:
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          role-to-assume: arn:aws:iam::<account-id>:role/github-terraform-role
          aws-region: ap-southeast-1

      - name: Rollback from last snapshot
        run: |
          latest_snapshot=$(aws rds describe-db-snapshots \
            --db-instance-identifier workshop-mysql \
            --query "reverse(sort_by(DBSnapshots, &SnapshotCreateTime))[0].DBSnapshotIdentifier" \
            --output text)

          aws rds restore-db-instance-from-db-snapshot \
            --db-instance-identifier workshop-mysql-rollback \
            --db-snapshot-identifier $latest_snapshot

      - name: Notify failure
        run: |
          aws sns publish \
            --topic-arn arn:aws:sns:ap-southeast-1:<account-id>:db-deploy-topic \
            --message "RDS deployment failed. Rolled back from snapshot." \
            --subject "RDS Deployment Failed"
```

- Once you have prepared and accurately edited the **ci-cd.yml** file, proceed to **Commit and push to GitHub**.

```bash
echo "# terraform-CICD-Workshop" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/TienTruong71/terraform-CICD-Workshop.git
git push -u origin main
```

![5](/images/imageAWS/512.png)  
![5](/images/imageAWS/513.png)  

{{%notice tip%}}
Once the **CMD** interface displays the notification like the image below, we have successfully completed the process!!
{{% /notice %}}

![5](/images/imageAWS/514.png)
