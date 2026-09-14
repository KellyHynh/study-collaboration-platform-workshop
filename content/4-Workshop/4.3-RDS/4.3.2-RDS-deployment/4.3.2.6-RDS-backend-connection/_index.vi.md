---

title: "Kết nối RDS với Backend"
date: 2026-09-14
weight: 6
chapter: false
pre: " <b> 4.3.2.6. </b> "
---

Sau khi cấu hình RDS, backend KnoVerse chạy trên EC2 cần được cập nhật để sử dụng cấu hình database của RDS.

#### Trước khi triển khai

Backend sử dụng PostgreSQL database trên local:

Backend

│

▼

Local PostgreSQL

#### Sau khi triển khai

Backend chạy trên EC2 kết nối đến PostgreSQL database trên RDS:

Backend on EC2

│

▼

RDS PostgreSQL

Backend sử dụng RDS endpoint thay cho:

localhost

hoặc database host của môi trường local.

Sau khi cập nhật database configuration, restart backend để áp dụng database connection mới.

![Backend RDS Configuration](/images/4-Workshop/4.3-RDS/image7.png)

