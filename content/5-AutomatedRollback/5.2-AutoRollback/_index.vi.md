---
title : "Triển khai tự động và Rollback"
date: 2025-07-22 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

- Trong phần 5 này, đầu tiên ta sẽ tạo **Repository Github** để có chỗ chứa môi trường chạy CI/CD.

### Tạo Repository trên Github

#### Bước 1: Đăng nhập vào GitHub
1. Truy cập [https://github.com](https://github.com).
2. Đăng nhập bằng tài khoản GitHub của bạn.

---

#### Bước 2: Tạo Repository mới
1. Ở góc trên bên phải, nhấn nút **`+`** → chọn **"New repository"**.
2. Điền thông tin:
   - **Repository name**: Tên repo (ví dụ: `terraform CICD Workshop`).
   - **Description** *(tùy chọn)*
   - **Visibility**:
     - `Public`: Ai cũng có thể xem.
     - `Private`: Chỉ bạn (và người được mời) mới xem được.
   - **Initialize this repository with**:
     - Chọn **Add a README file** nếu muốn tạo file README.md ngay.
     - Chọn **Add .gitignore** để bỏ qua file/thư mục không cần push.
     - Chọn **Choose a license** nếu muốn thêm giấy phép sử dụng.

![5](/images/imageAWWS/51.png)

---

#### Bước 3: Hoàn tất tạo Repository
- Nhấn **Create repository**.
- Bạn sẽ được chuyển đến trang repo vừa tạo.


### Triển khai CICD

#### Tạo cấu trúc thư mục trong **visual studio**
- Tạo file `ci-cd.yml` nằm trong folder **.github\workflows**, tương tự như ảnh bên dưới

![5](/images/imageAWWS/511.png)

#### Nội dung file **ci-cd.yml**

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

-  khi đã chuản bị và sửa lại chính xác toàn bộ file **ci-cd.yml**, ta tiến hành thực hiện bước **Commit và push lên github**

```bash
echo "# terraform-CICD-Workshop" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/TienTruong71/terraform-CICD-Workshop.git
git push -u origin main 
```
![5](/images/imageAWWS/512.png)
![5](/images/imageAWWS/513.png)

{{%notice tip%}}
Sau khi giao diện thông báo **CMD** như ảnh dưới đây là chúng ta đã thực hiện thành công!!
{{% /notice %}}

![5](/images/imageAWWS/514.png)
