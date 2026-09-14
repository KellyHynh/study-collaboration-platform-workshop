---

title: "Cấu hình Environment Variables"

date: 2026-09-14

weight: 7

chapter: false

pre: " <b> 4.4.2.7. </b> "

---

Backend cần được cấu hình với các environment variables phù hợp với môi trường AWS.

Đặc biệt, database configuration phải trỏ đến Amazon RDS thay vì PostgreSQL local.

Ví dụ:

DB_HOST=<RDS_ENDPOINT>

DB_PORT=5432

DB_NAME=<DATABASE_NAME>

DB_USER=<DATABASE_USER>

DB_PASSWORD=<DATABASE_PASSWORD>

Các application configuration khác cũng được thiết lập tương ứng với deployment environment.

Không đưa password hoặc secret trực tiếp vào source code.

