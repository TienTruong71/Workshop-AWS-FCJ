---
title : "Triển khai tự động & Rollback"
date: 2025-07-22 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

Trong phần này, chúng ta sẽ thiết lập **quy trình triển khai ứng dụng tự động** (CI/CD) và cơ chế **rollback** khi có lỗi xảy ra.  
Mục tiêu là đảm bảo rằng mỗi thay đổi mã nguồn được đưa lên repository sẽ được triển khai một cách nhanh chóng, an toàn và có khả năng khôi phục về phiên bản ổn định trước đó nếu gặp sự cố.

### Mục tiêu
- Cấu hình pipeline để tự động build, test và deploy ứng dụng.
- Thiết lập trigger triển khai khi có commit mới lên nhánh chính (**main branch**).
- Áp dụng chiến lược rollback để giảm thiểu thời gian downtime khi triển khai thất bại.
- Thử nghiệm quá trình rollback để đảm bảo khả năng khôi phục.

### Kết quả đạt được
Kết thúc phần này, bạn sẽ nắm được:
1. Toàn bộ quy trình **tự động hóa triển khai** từ commit đến môi trường production.
2. Cách tích hợp **cơ chế rollback** nhằm bảo vệ hệ thống trước rủi ro khi release phiên bản mới.
3. Kỹ năng thực hành rollback an toàn và nhanh chóng.

### Nội dung:

  - [Tạo Role IAM](./5.1-CreateRoleIAm/)
  - [Triển khai tự động và Rollback](./5.2-AutoRollback/)