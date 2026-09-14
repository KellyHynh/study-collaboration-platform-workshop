---

title: "Kết nối EC2 với Amazon RDS"

date: 2026-09-14

weight: 8

chapter: false

pre: " <b> 4.4.2.8. </b> "

---

Sau khi environment variables được cấu hình, backend chạy trên EC2 thực hiện kết nối đến RDS.

Luồng kết nối:

EC2

 │

 │ TCP 5432

 ▼

RDS PostgreSQL

#### Kiểm tra kết nối

Kiểm tra các thông tin sau:

- RDS đang ở trạng thái **Available**.

- RDS endpoint chính xác.

- Port 5432 được cho phép.

- EC2 Security Group và RDS Security Group cho phép traffic cần thiết.

- Database credentials chính xác.

Sau khi kết nối thành công, backend có thể thực hiện các database queries.

