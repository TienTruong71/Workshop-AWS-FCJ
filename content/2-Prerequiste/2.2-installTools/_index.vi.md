---
title : "Cài đặt các công cụ cần thiết"
date: 2025-07-22 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

### Cài đặt các công cụ cần thiết

Trong bước này chúng ta sẽ cài đặt những công cụ cần thiết để tiến hành bài lab 

![Tool](/images/imageAWS/tool.drawio.png)

## 1. Cài đặt Visual Studio Code (VS Code)

### Bước 1: Tải Visual Studio Code
- Truy cập: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- Bấm **Download for Windows**.

![Tool](/images/imageAWS/tool1.png)


### Bước 2: Cài đặt
1. Mở file `.exe` vừa tải về.
2. Chọn **I accept the agreement** → **Next**.
3. Chọn thư mục cài đặt (mặc định `C:\Program Files\Microsoft VS Code`) → **Next**.
4. Tick **Add to PATH** và **Register Code as an editor**.
5. Bấm **Install** → **Finish**.

### Bước 3: Cài đặt Extensions
Mở VS Code → **Extensions** (Ctrl + Shift + X) → cài:
- `HashiCorp Terraform`
- `AWS Toolkit`
- `Prettier`
- `GitLens`

---

## 2. Cài đặt Terraform

### Bước 1: Tải Terraform
- Truy cập: [https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)
- Chọn **Windows → AMD64** (hoặc ARM nếu máy bạn dùng chip ARM).

![Tool](/images/imageAWS/tool2.png)


### Bước 2: Giải nén & Thêm vào PATH
1. Giải nén file `.zip` vào thư mục, ví dụ: `C:\terraform`.
2. Mở **Control Panel** → **System** → **Advanced system settings**.
3. Chọn **Environment Variables**.
4. Ở **System variables**, tìm **Path** → **Edit** → **New** → nhập `C:\terraform`.
5. Bấm **OK**.

### Bước 3: Kiểm tra cài đặt
```bash
terraform -version
```
nếu hiển thị phiên bản terraform -> cài đặt thành công 

---

## 3. Cài đặt AWS CLI

### Bước 1 : Tải AWS CLI
- Truy cập trang tải chính thức: [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
- Chọn **Download for Windows (64-bit)**.

### Bước 2: Cài đặt AWS CLI

1. Mở file `.msi` vừa tải về.
2. Chọn **Next**.
3. Tick **I accept the terms in the License Agreement** → **Next**.
4. Chọn thư mục cài đặt (mặc định: `C:\Program Files\Amazon\AWSCLI`) → **Next**.
5. Nhấn **Install**.
6. Khi cài xong, nhấn **Finish**.

---

## Bước 3: Kiểm tra cài đặt

Mở **Command Prompt** hoặc **PowerShell**, chạy:
```bash
aws --version
```
Nếu hiển thị phiên bản AWS CLI (ví dụ aws-cli/2.x.x) → cài đặt thành công.

### Bước 4: Cấu hình AWS CLI 

chạy lệnh :

```bash
aws configure
```
Nhập thông tin:
  + AWS Access Key ID → lấy từ IAM trên AWS.
  + AWS Secret Access Key → lấy từ IAM trên AWS.
  + Default region name → ví dụ: ap-southeast-1 (Singapore).
  + Default output format → json.


### Bước 5. Kiểm tra kết nối với AWS 
chạy :
```bash
aws s3 ls
```
Nếu hiển thị danh sách bucket S3 -> cấu hình thành công 

Vậy là chúng ta đã hoàn thành việc cài đặt tất cả những công cụ cần thiết, bước tiếp theo ta sẽ dựa vào những công cụ đó và tiến đến phần 3 **Phát triển hạ tầng IaC cho Database**