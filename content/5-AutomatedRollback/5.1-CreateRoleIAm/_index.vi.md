---
title : "Tạo Role IAM"
date: 2025-07-22 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

### Tạo **IAM Role** cho Github Actions:
- Ở giao diện **IAM** click chọn **Roles** trong danh mục sidebar bên trái  
- Ấn **Create Role** để tiến hành khởi tạo

![5](/images/imageAWWS/52.png)

### bước 1: **Select trusted entity** 
- Tại mục **Trusted entity type**, click chọn **Web identity**.
- Tại mục **Web identity**, click **Create new** để tạo provider là github

![5](/images/imageAWWS/53.png)

### Tại giao diện **Add Identity Provider**
- Tại mục **Provider details**, đầu tiên chọn **OpenID Connect** tại hộp thoại **Provider type**.
- Tại mục **Provider URL**, điền `https://token.actions.githubusercontent.com`.
- Tại mục **Audience**, điền `sts.amazonaws.com`.
- Sau đó ấn **Add Provider**.

![5](/images/imageAWWS/54.png)

### Quay về giao diện **bước 1**
- Click chọn vào Provider vừa tạo là **token.actions.githubusercontent.com**

![5](/images/imageAWWS/55.png)

- Sau khi đã chọn Provider, lần lượt điền các mục trong ô nhập như sau 
+ Identity : `token.actions.githubusercontent.com`
+ Audience : `sts.amazonaws.com`
+ 2 mục cuối điền *.
+ Kéo con trỏ chuột xuống bấm **Next**

![5](/images/imageAWWS/56.png)

### Bước 2 : Add Permissions 
- tại giao diện mục **Permissions polices** lần lượt tìm và gắn các quyền sau
 - `AmazonRDSFullAccess`
 - `AmazonSSMFullAccess`
 - `CloudWatchLogsFullAccess`
 - `AmazonSNSFullAccess`
 - Sau khi đã thêm đủ quyền, ấn **Next** để qua bước cuối cùng.
 - ví dụ: 

![5](/images/imageAWWS/57.png)

### Bước 3 : Name, review, and create.

- Tại mục **Role name**, điền `github-actions-deploy-role`.
- Tại mục **Description**, nhập `IAM role for GitHub Actions OIDC access to deploy infrastructure`.

![5](/images/imageAWWS/58.png)

- Kiểm tra lại lần nữa xem đã gán đủ quyền và còn sai sót gì nữa không, sau đó bấm **Create Role** để khởi tạo.

![5](/images/imageAWWS/59.png)

- Giao diện màn hình đã khởi tạo **IAM Role** thành công

![5](/images/imageAWWS/510.png)


