---

title: "Chuẩn bị và xác định yêu cầu"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.3.2.1. </b> "

---

Trước khi tạo Amazon RDS instance, cần xác định các yêu cầu cơ bản về database và networking.

#### Yêu cầu về Database và Network

Các thông tin sau được sử dụng cho quá trình triển khai RDS của KnoVerse:

| **Thành phần**  | **Giá trị**                  |
| --------------- | ---------------------------- |
| Database Engine | PostgreSQL                   |
| AWS Region      | ap-southeast-1               |
| VPC             | KnoVerse VPC                 |
| Database Port   | 5432                         |
| Application     | KnoVerse Backend             |
| Database Client | PostgreSQL-compatible client |

Các giá trị này cung cấp cấu hình cơ bản cần thiết để triển khai PostgreSQL database và kết nối database với KnoVerse backend.

#### Thông tin cần chuẩn bị

Trước khi tạo RDS database, cần chuẩn bị các thông tin sau:

- Database name.

- Master username.

- Master password.

- Database schema.

- Database seed/demo data nếu cần.

- Security Group cho database.

Database credentials cần được chuẩn bị trước và lưu trữ an toàn. Không đưa password thực tế trực tiếp vào source code, screenshot hoặc repository.

