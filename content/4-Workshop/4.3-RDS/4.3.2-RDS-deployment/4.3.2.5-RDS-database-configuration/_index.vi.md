---

title: "Cấu hình Database"
date: 2026-09-14
weight: 5
chapter: false
pre: " <b> 4.3.2.5. </b> "
---

Sau khi RDS instance sẵn sàng và cấu hình network đã hoàn tất, cần chuẩn bị cấu hình database để backend KnoVerse sử dụng.

#### Cấu hình Database

Xác định các thông tin kết nối database sau:

Database name

Username

Password

Host

Port

Cấu hình backend có thể được biểu diễn như sau:

DB_HOST=<RDS_ENDPOINT>

DB_PORT=5432

DB_NAME=<DATABASE_NAME>

DB_USER=<DATABASE_USER>

DB_PASSWORD=<DATABASE_PASSWORD>

Các giá trị thực tế cần được cấu hình trong environment của backend.

**Không đưa password thực tế vào source code, screenshot hoặc repository.**

