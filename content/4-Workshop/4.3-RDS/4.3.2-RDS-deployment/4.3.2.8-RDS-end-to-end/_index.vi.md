---

title: "Kiểm tra End-to-End"
date: 2026-09-14
weight: 8
chapter: false
pre: " <b> 4.3.2.8. </b> "
---

Bước này xác nhận toàn bộ quá trình triển khai database hoạt động từ application đến RDS.

Luồng kiểm tra:

![RDS End-to-End Flow](images/4-Workshop/4.3-RDS/image10.png)

#### Bước 1 — Kiểm tra Backend

Đảm bảo backend chạy trên EC2 đang hoạt động bình thường.

#### Bước 2 — Gửi API Request

Thực hiện request đến endpoint:

GET /api/courses

#### Bước 3 — Kiểm tra Response

API phải trả về HTTP success response và course data.

Ví dụ:

HTTP/1.1 200 OK

Content-Type: application/json

#### Bước 4 — Đối chiếu với Database

Kiểm tra dữ liệu trả về từ API có tương ứng với dữ liệu được lưu trong RDS hay không.

Nếu API trả về course data thành công, có thể xác nhận luồng sau đã hoạt động:

Backend

↓

Database connection

↓

RDS PostgreSQL

↓

Database query

↓

API response

Toàn bộ flow đã hoạt động end-to-end.

![RDS Verification Result](images/4-Workshop/4.3-RDS/11.png)

