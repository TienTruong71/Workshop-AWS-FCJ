# Database Configuration Management & Infrastructure as Code (IaC)
## Automating Infrastructure and Database Lifecycle with DevOps Best Practices

---

# Tóm tắt Dự án

Tài liệu này trình bày đề xuất chi tiết cho một workshop chuyên sâu về **quản lý cấu hình cơ sở dữ liệu và hạ tầng dưới dạng mã (Infrastructure as Code - IaC)** trên nền tảng AWS. Mục tiêu là giúp người học nắm bắt cách sử dụng các công cụ như **Terraform** và **Liquibase/Flyway** để tự động hóa việc triển khai cơ sở dữ liệu, đồng bộ môi trường, kiểm soát version của schema, và tích hợp vào pipeline CI/CD.

Thông qua workshop, học viên sẽ hiểu được cách thiết kế hạ tầng linh hoạt, bảo mật, có khả năng mở rộng, đồng thời quản lý thay đổi cấu trúc dữ liệu một cách kiểm soát và minh bạch.

---

# 1. Vấn đề Đặt ra

## Tình hình Hiện tại
- Việc thay đổi database vẫn được thực hiện thủ công.
- Không có quy trình version hóa schema rõ ràng.
- Dễ xảy ra sai lệch giữa môi trường dev, staging và production.

## Thách thức Chính
- Thiếu công cụ tự động và chuẩn hóa quy trình.
- Nguy cơ lỗi cao và khó rollback nếu gặp sự cố.
- Triển khai sản phẩm bị trì hoãn do lỗi cấu hình.

## Tác động tới Các bên liên quan
- Dev gặp lỗi do môi trường không đồng bộ.
- DevOps khó kiểm soát và tái tạo môi trường.
- Ban điều hành gặp rào cản trong quá trình ra mắt sản phẩm mới.

## Hệ quả Kinh doanh
- Tăng chi phí bảo trì và khắc phục sự cố.
- Giảm tốc độ phát triển và đổi mới.
- Rủi ro downtime cao hơn.

---

# 2. Kiến trúc Giải pháp

## Tổng quan Kiến trúc
- Sử dụng **Terraform** để tự động hóa việc triển khai hạ tầng AWS (VPC, RDS, IAM…).
- Dùng **Liquibase hoặc Flyway** để quản lý schema và migration.
- Triển khai CI/CD tích hợp Git để đảm bảo nhất quán và kiểm soát thay đổi.

## Dịch vụ AWS Sử dụng
- **Amazon RDS** – quản lý cơ sở dữ liệu
- **AWS S3** – lưu trữ file migration
- **AWS IAM** – phân quyền truy cập
- **AWS CloudWatch** – giám sát và log
- (Tùy chọn) **AWS CloudFormation**

## Thiết kế Thành phần
- Terraform được tổ chức theo module: network, database, IAM.
- Pipeline CI/CD chứa các bước kiểm tra và thực thi schema migration.

## Kiến trúc Bảo mật
- Database đặt trong private subnet.
- Dùng IAM role giới hạn truy cập.
- Secrets được lưu trữ bằng AWS Secrets Manager.

## Thiết kế Khả năng Mở rộng
- Hỗ trợ triển khai nhiều môi trường độc lập.
- RDS Multi-AZ cho độ sẵn sàng cao.
- Pipeline và module dễ dàng tái sử dụng.

---

# 3. Triển khai Kỹ thuật

## Các Giai đoạn Triển khai
1. Cấu hình môi trường AWS và công cụ cần thiết.
2. Viết module Terraform tạo hạ tầng và RDS.
3. Tích hợp quản lý schema bằng Liquibase/Flyway.
4. Tạo pipeline CI/CD triển khai môi trường.
5. Demo chạy thực tế môi trường staging.

## Yêu cầu Kỹ thuật
- Terraform >= v1.3
- AWS CLI
- Liquibase hoặc Flyway
- Git, GitHub Actions hoặc GitLab CI

## Cách Tiếp cận Phát triển
- Mô hình GitOps: mọi thay đổi được quản lý qua Git và CI/CD.
- Từng bước nhỏ, kiểm tra liên tục trước khi đưa vào production.

## Chiến lược Kiểm thử
- Kiểm thử `terraform plan` trước khi `apply`.
- Kiểm thử migration script với database độc lập.

## Kế hoạch Triển khai
- Terraform apply hạ tầng trước.
- CI chạy migration và kiểm tra schema.
- Manual approval cho môi trường production.

---

# 4. Thời gian & Mốc Triển khai

## Lịch trình Dự án

| Giai đoạn | Thời gian | Tuần |
|-----------|-----------|------|
| Chuẩn bị & Setup ban đầu | 1 tuần | Tuần 1 |
| Viết module Terraform | 1 tuần | Tuần 2 |
| Tích hợp Liquibase & CI/CD | 1 tuần | Tuần 3 |
| Triển khai demo | 1 tuần | Tuần 4 |
| Đánh giá & hoàn thiện | 1 tuần | Tuần 5 |

## Mốc Chính
- Module Terraform hoạt động đúng.
- Pipeline CI/CD tự động hóa migration.
- Demo thành công môi trường staging.

## Phụ thuộc
- Có tài khoản AWS.
- Có công cụ CI/CD đang hoạt động.
- Học viên có kiến thức cơ bản về Git và Terraform.

## Phân bổ Nguồn lực
- 1 Giảng viên chính (DevOps)
- 1 Trợ giảng hỗ trợ kỹ thuật
- Môi trường AWS sandbox

---

# 5. Ước lượng Ngân sách

## Chi phí Hạ tầng
- RDS: ~50$/tháng (hoặc Free Tier)
- Networking & S3: ~10–15$/tháng

## Chi phí Phát triển
- Chuẩn bị bài giảng 
- Soạn slide & lab thực hành

## Chi phí Vận hành
- Hosting workshop, tài khoản AWS: ~30$
- CI/CD runner: Miễn phí với GitHub Actions

## Phân tích Lợi tức (ROI)
- Giảm thời gian setup môi trường đến 80%.
- Tăng tốc độ release phần mềm.
- Tiết kiệm chi phí vận hành lâu dài.

---

# 6. Đánh giá Rủi ro

## Ma trận Rủi ro

| Rủi ro | Khả năng xảy ra | Mức ảnh hưởng |
|--------|------------------|----------------|
| Chi phí AWS vượt kiểm soát | Thấp | Trung bình |
| Terraform khó học với người mới | Trung bình | Cao |
| Lỗi migration xóa mất dữ liệu | Thấp | Cao |

## Chiến lược Giảm thiểu
- Dùng Free Tier và AWS Budget Alerts.
- Soạn hướng dẫn Terraform cơ bản cho người học.
- Backup schema trước khi migration.

## Kế hoạch Dự phòng
- Dùng database local nếu AWS bị giới hạn.
- Thực hiện migration thủ công khi cần.
- Snapshot dữ liệu quan trọng.

---

# 7. Kết quả Kỳ vọng

## Chỉ số Thành công
- Hạ tầng được provision bằng Terraform.
- CI/CD chạy migration thành công.
- Học viên hoàn thành labs trong thời gian quy định.

## Lợi ích Kinh doanh
- Tăng độ ổn định của hệ thống backend.
- Giảm rủi ro khi deploy database.
- Chuẩn hóa môi trường và quy trình DevOps.

## Cải tiến Kỹ thuật
- Cấu hình DB có thể kiểm soát và lặp lại.
- Sử dụng IaC chuẩn hóa toàn bộ hệ thống.

## Giá trị Dài hạn
- Có thể tái sử dụng trong các dự án khác.
- Giảm thời gian onboard team mới.
- Tạo nền tảng cho DevOps chuyên sâu.

---

# Phụ lục

## A. Thông số Kỹ thuật
- Terraform >= v1.4
- Database: MySQL
- CI/CD: GitHub Actions hoặc GitLab CL

## B. Tính toán Chi phí
- Chi tiết trong file `/docs/budget.xlsx`

## C. Sơ đồ Kiến trúc
- Có trong thư mục `/diagrams/infra.png`
- CI/CD flow: `/diagrams/pipeline.png`

## D. Tài liệu Tham khảo
- [Hướng dẫn Terraform AWS Modules](https://registry.terraform.io/namespaces/terraform-aws-modules)
- [So sánh Liquibase & Flyway](https://www.baeldung.com/liquibase-flyway)
- [Tài liệu chính thức về IaC từ AWS](https://docs.aws.amazon.com/whitepapers/latest/infrastructure-as-code/introduction.html)
