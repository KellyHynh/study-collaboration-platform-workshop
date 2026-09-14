---

title: "Cấu hình Security Group"
date: 2026-09-14
weight: 4
chapter: false
pre: " <b> 4.3.2.4. </b> "
---

Security Group kiểm soát traffic đến RDS instance và xác định các resource được phép thiết lập kết nối đến database.

#### Bước 1 — Mở Security Group

Từ phần **Connectivity & security**, mở Security Group được gắn với RDS instance.

#### Bước 2 — Cấu hình Inbound Rule

Thêm inbound rule cho PostgreSQL:

Type:

PostgreSQL

Protocol: TCP

Port: 5432

Source: Security Group của backend EC2

Khi sử dụng Security Group của EC2 làm source, RDS chỉ cho phép các resource thuộc Security Group đó thiết lập kết nối đến database.

Không nên mở database port cho tất cả các nguồn.

Không sử dụng:

0.0.0.0/0

cho PostgreSQL trong môi trường triển khai thực tế.

#### Bước 3 — Kiểm tra Outbound Rules

Đảm bảo outbound configuration không ngăn cản các connection cần thiết.

![RDS Security Group](images/4-Workshop/4.3-RDS/image6.png)

