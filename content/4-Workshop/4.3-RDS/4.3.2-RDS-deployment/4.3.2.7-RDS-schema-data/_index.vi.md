---

title: "Khởi tạo Schema và dữ liệu"
date: 2026-09-14
weight: 7
chapter: false
pre: " <b> 4.3.2.7. </b> "
---

Sau khi backend có thể kết nối đến RDS, có thể tiến hành khởi tạo database schema của KnoVerse.

#### Bước 1 — Kết nối đến RDS PostgreSQL

Sử dụng PostgreSQL client hoặc database tool phù hợp để kết nối đến RDS endpoint.

#### Bước 2 — Tạo Database Structure

Thực hiện database migration hoặc chạy schema initialization script của KnoVerse.

![Khởi tạo RDS Database](images/4-Workshop/4.3-RDS/image8.png)

#### Bước 3 — Kiểm tra Tables

Xác nhận tất cả các table cần thiết đã được tạo thành công.

#### Bước 4 — Import dữ liệu

Nếu workshop sử dụng dữ liệu mẫu, thực hiện seed hoặc import dữ liệu vào database.

#### Bước 5 — Kiểm tra Relationships

Kiểm tra các relationships và constraints của database:

- Primary keys.

- Foreign keys.

- Unique constraints.

- Các relationships giữa các bảng.

![RDS Database Tables](images/4-Workshop/4.3-RDS/image9.png)

