---
title : "Install Tools Required"
date: 2025-07-22
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

### Install Required Tools

In this step, we will install the necessary tools to proceed with the lab.

![Tool](/images/imageAWS/tool.drawio.png)

## 1. Install Visual Studio Code (VS Code)

### Step 1: Download Visual Studio Code
- Go to: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- Click **Download for Windows**.

![Tool](/images/imageAWS/tool1.png)

### Step 2: Installation
1. Open the downloaded `.exe` file.
2. Select **I accept the agreement** → **Next**.
3. Choose the installation folder (default: `C:\Program Files\Microsoft VS Code`) → **Next**.
4. Tick **Add to PATH** and **Register Code as an editor**.
5. Click **Install** → **Finish**.

### Step 3: Install Extensions
Open VS Code → **Extensions** (Ctrl + Shift + X) → install:
- `HashiCorp Terraform`
- `AWS Toolkit`
- `Prettier`
- `GitLens`

---

## 2. Install Terraform

### Step 1: Download Terraform
- Go to: [https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)
- Choose **Windows → AMD64** (or ARM if your machine uses ARM chip).

![Tool](/images/imageAWS/tool2.png)

### Step 2: Extract & Add to PATH
1. Extract the `.zip` file to a folder, e.g., `C:\terraform`.
2. Open **Control Panel** → **System** → **Advanced system settings**.
3. Click **Environment Variables**.
4. In **System variables**, find **Path** → **Edit** → **New** → enter `C:\terraform`.
5. Click **OK**.

### Step 3: Verify Installation
```bash
terraform -version
```
If the Terraform version is displayed → installation successful.

---

## 3. Install AWS CLI
### Step 1:  Download AWS CLI
  + Go to: [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
  + Select Download for Windows (64-bit).
### Step 2: Installation
1. Open the downloaded .msi file.
2. Click Next.
3. Tick I accept the terms in the License Agreement → Next.
4. Choose the installation folder (default: C:\Program Files\Amazon\AWSCLI) → Next.
5. Click Install.
6. When done, click Finish.
## Step 3: Check Installation
Open **Command Prompt** or **PowerShell**, run:
```bash
aws --version
```
If the AWS CLI version is displayed (e.g., aws-cli/2.x.x) → installation successful.
### Step 4: Configure AWS CLI
Run the command:
```bash
aws configure
```
Enter the information:
+ AWS Access Key ID → obtained from IAM on AWS.
+ AWS Secret Access Key → obtained from IAM on AWS.
+ Default region name → for example: ap-southeast-1 (Singapore).
+ Default output format → json.
### Step 5: Check connection to AWSRun:
```bash
aws s3 ls
```
If the list of S3 buckets is displayed -> configuration successful.
We have now completed the installation of all required tools.
In the next step, we will use these tools to proceed to Part 3: Developing IaC Infrastructure for the Database.