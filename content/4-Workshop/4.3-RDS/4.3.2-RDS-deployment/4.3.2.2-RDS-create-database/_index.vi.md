---

title: "Tạo PostgreSQL Database trên Amazon RDS"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 4.3.2.2. </b> "
---


Phần này trình bày quy trình tạo PostgreSQL database trên Amazon RDS cho backend KnoVerse.

#### Bước 1 — Mở Amazon RDS

Truy cập AWS Management Console và mở **Amazon RDS**.

Đảm bảo Region được chọn là:

Asia Pacific (Singapore)

ap-southeast-1

![Mở Amazon RDS](images/4-Workshop/4.3-RDS/image2.png)

#### Bước 2 — Tạo Database

Chọn:

**Databases → Create database**

Chọn phương thức triển khai phù hợp với mục đích của workshop.

#### Bước 3 — Chọn Database Engine

Tại phần Engine options:

Engine type:

PostgreSQL

Chọn phiên bản PostgreSQL tương thích với ứng dụng.

Nếu database local đang sử dụng một phiên bản PostgreSQL cụ thể, nên chọn phiên bản tương thích để hạn chế các vấn đề có thể xảy ra trong quá trình migrate database.
![RDS Connectivity and Endpoint](images/4-Workshop/4.3-RDS/image3.png)

#### Bước 4 — Cấu hình Database Credentials

Thiết lập:

- DB instance identifier.

- Master username.

- Master password.

Password cần được lưu trữ an toàn và không được đưa trực tiếp vào source code.

#### Bước 5 — Cấu hình Compute và Storage

Chọn instance class và storage configuration phù hợp với quy mô của workshop.

Đối với môi trường học tập hoặc demo, nên ưu tiên cấu hình nhỏ và phù hợp với Free Tier hoặc AWS credits hiện có.

#### Bước 6 — Tạo Database

Kiểm tra lại cấu hình và chọn:

**Create database**

Chờ database chuyển sang trạng thái available.

![RDS Connectivity and Endpoint](images/4-Workshop/4.3-RDS/image4.png)
