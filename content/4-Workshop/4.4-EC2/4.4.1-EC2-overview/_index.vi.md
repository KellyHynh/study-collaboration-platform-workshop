---

title: "Tổng quan về EC2"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.4.1. </b> "

---

Amazon EC2 được sử dụng trong kiến trúc KnoVerse để triển khai và vận hành backend application trên AWS. EC2 cung cấp compute layer, chịu trách nhiệm chạy Node.js/Express backend, xử lý API requests và giao tiếp với Amazon RDS.

#### 4.4.1.1. Mục đích sử dụng Amazon EC2

Amazon EC2 cung cấp một virtual server trên AWS để chạy backend của KnoVerse.

Backend chạy trên EC2 chịu trách nhiệm:

- Chạy Node.js application.

- Xử lý HTTP requests.

- Cung cấp REST API cho frontend.

- Thực hiện các CRUD operations.

- Kết nối và truy vấn dữ liệu từ Amazon RDS.

- Cung cấp application endpoint cho Application Load Balancer.

Sau khi triển khai, backend không còn phụ thuộc vào máy local của developer để phục vụ application.

#### 4.4.1.2. Tại sao chọn Amazon EC2?

Amazon EC2 được lựa chọn vì cho phép backend application chạy trong một compute environment có khả năng kiểm soát tương đối đầy đủ đối với server configuration.

Các lý do chính bao gồm:

- Có thể lựa chọn operating system và instance configuration theo yêu cầu của application.

- Có thể cài đặt Node.js và các dependencies cần thiết cho KnoVerse.

- Có thể kiểm soát application runtime và process.

- EC2 có thể dễ dàng kết nối với RDS trong cùng VPC.

- EC2 có thể được tích hợp với Application Load Balancer.

- Có thể mở rộng hoặc thay đổi instance configuration khi hệ thống phát triển.

Đối với một project học tập như KnoVerse, EC2 cũng giúp minh họa rõ cách một backend application được đưa từ local environment lên cloud infrastructure.

#### 4.4.1.3. Vai trò trong kiến trúc KnoVerse

EC2 nằm giữa Application Load Balancer và Amazon RDS trong kiến trúc backend:

![KnoVerse EC2 Architecture](/images/4-Workshop/4.4-EC2/1.png)

Các thành phần chính bao gồm:

- CloudFront: phân phối và tiếp nhận requests từ client.

- Application Load Balancer: nhận HTTP requests và định tuyến đến backend.

- EC2: chạy KnoVerse backend.

- RDS: lưu trữ dữ liệu PostgreSQL.

EC2 vì vậy đóng vai trò là application layer và compute layer của hệ thống KnoVerse.

