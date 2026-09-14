---

title: "Kiểm tra RDS"
date: 2026-09-14
weight: 4
chapter: false
pre: " <b> 4.3.3. </b> "
---

Sau khi hoàn thành triển khai Amazon RDS, database cần được kiểm thử và đánh giá để đảm bảo hoạt động chính xác với backend KnoVerse.

#### 4.3.3.1. Kiểm thử kết nối và chức năng

Các kiểm thử chính bao gồm:

| **Kiểm thử**            | **Kết quả mong đợi**       |
| ----------------------- | -------------------------- |
| EC2 → RDS               | Kết nối thành công         |
| PostgreSQL port 5432    | Có thể truy cập từ backend |
| Database authentication | Thành công                 |
| Database query          | Trả về dữ liệu             |
| Backend → RDS           | Thành công                 |
| GET /api/courses        | HTTP 200 OK                |
| Course data             | Trả về đúng dữ liệu        |

Các kiểm thử này giúp xác định database layer hoạt động đúng trước khi tiếp tục tích hợp với các AWS services khác.

#### 4.3.3.2. Đánh giá cấu hình

Sau deployment, configuration của RDS cần được đánh giá dựa trên:

- Database availability.

- Network connectivity.

- Security Group configuration.

- Storage configuration.

- Compute configuration.

- Database accessibility.

- Application compatibility.

Đối với môi trường workshop, cấu hình được lựa chọn theo hướng đơn giản và tiết kiệm chi phí, trong khi vẫn đáp ứng được nhu cầu của KnoVerse.

#### 4.3.3.3. Xử lý các vấn đề

Trong quá trình triển khai database trên cloud, một số vấn đề có thể xảy ra.

**Không thể kết nối EC2 → RDS**

Kiểm tra theo thứ tự:

1. RDS có trạng thái Available.

2. EC2 và RDS có network configuration phù hợp.

3. Security Group của RDS cho phép TCP port 5432.

4. Source của inbound rule cho phép Security Group của backend EC2.

5. Database credentials chính xác.

6. RDS endpoint chính xác.

**Backend vẫn sử dụng database local**

Kiểm tra environment variables của backend và đảm bảo:

DB_HOST

đang trỏ đến RDS endpoint thay vì localhost.

**API không trả dữ liệu**

Kiểm tra:

- Database schema.

- Seed data.

- Database connection.

- SQL queries.

- Backend logs.

#### 4.3.3.4. Phương án tối ưu

Khi hệ thống KnoVerse phát triển, RDS có thể được tối ưu theo nhu cầu thực tế.

Các hướng mở rộng có thể bao gồm:

- Điều chỉnh DB instance class.

- Tăng hoặc tối ưu storage.

- Cấu hình backup phù hợp.

- Sử dụng Multi-AZ cho yêu cầu availability cao hơn.

- Tối ưu database indexes và queries.

- Theo dõi database metrics bằng Amazon CloudWatch.

- Sử dụng caching layer như Amazon ElastiCache khi application có nhu cầu giảm database load.

Các phương án này không nhất thiết phải được triển khai trong workshop cơ bản mà được xem là các hướng mở rộng cho hệ thống trong tương lai.

#### 4.3.3.5. Kết quả đạt được

Sau khi hoàn thành deployment, Amazon RDS đã đảm nhiệm database layer của KnoVerse.

Kết quả chính:

- PostgreSQL database được triển khai trên Amazon RDS.

- Database được tích hợp với VPC của hệ thống.

- Security Group kiểm soát database traffic.

- Backend trên Amazon EC2 kết nối được với RDS.

- Database schema và dữ liệu KnoVerse được thiết lập.

- Backend có thể thực hiện database queries.

- Endpoint /api/courses trả về course data thành công.

- Database layer hoạt động cùng với application layer trên AWS.

Kiến trúc sau khi hoàn thành RDS deployment:

![RDS Architecture](images/4-Workshop/4.3-RDS/image1.png)

