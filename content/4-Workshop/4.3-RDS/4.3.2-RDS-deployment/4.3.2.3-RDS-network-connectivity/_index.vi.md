---

title: "Cấu hình Network và Connectivity"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.3.2.3. </b> "
---


Sau khi tạo database, cần xác định và kiểm tra cấu hình network để backend chạy trên EC2 có thể kết nối đến RDS.

#### Bước 1 — Mở Connectivity & Security

Trong RDS database, mở:

**Connectivity & security**

Kiểm tra các thông tin sau:

- VPC.

- Availability Zone.

- Subnet.

- Security Group.

- Endpoint.

- Port.

Database endpoint có dạng tương tự:

<database-identifier>.<random-id>.<region>.rds.amazonaws.com

Port PostgreSQL mặc định là:

5432

#### Bước 2 — Xác định Endpoint

Endpoint sẽ được sử dụng làm **DB_HOST** trong backend.

Ví dụ:

DB_HOST=<RDS_ENDPOINT>

DB_PORT=5432

![RDS Connectivity and Endpoint](images/4-Workshop/4.3-RDS/image5.png)

