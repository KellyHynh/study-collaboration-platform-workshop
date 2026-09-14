---
title: "Prepare and Configure ALB"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.5.2.1. </b> "
---

#### 4.5.2.1. Chuẩn bị trước khi tạo ALB

Trước khi tạo ALB, cần đảm bảo:

- EC2 instance đã được tạo.
- Backend application đang chạy.
- Backend lắng nghe đúng port.
- VPC đã được cấu hình.
- Có ít nhất hai Availability Zones/subnets phù hợp cho ALB.
- Security Groups đã được chuẩn bị.

Trong KnoVerse, backend hiện chạy trên:

EC2 → port 3000

ALB sẽ tiếp nhận HTTP request trên:

ALB → port 80

và chuyển tiếp đến:

EC2 → port 3000

#### 4.5.2.2. Tạo Target Group

Target Group xác định backend target mà ALB sẽ forward request tới.

Vào:

**EC2 → Target Groups → Create target group**

Chọn:

Target type: Instances

Protocol: HTTP

Port: 3000

Đặt tên, ví dụ:

knoverse-backend-tg

Chọn VPC đang sử dụng cho KnoVerse.

#### 4.5.2.3. Cấu hình Health Check

Health Check được sử dụng để xác định target có đang hoạt động hay không.

Cấu hình:

Protocol: HTTP

Port: Traffic port

Path: /api/courses

Nếu /api/courses trả về response thành công, target có thể được xác định là healthy.

Có thể sử dụng một endpoint health riêng trong tương lai, ví dụ:

GET /health

Nhưng với implementation hiện tại, /api/courses có thể được sử dụng để xác nhận backend đang phản hồi.


#### 4.5.2.4. Register EC2 Instance vào Target Group

Ở bước **Register targets**, chọn EC2 instance của KnoVerse.

Chọn port:

3000

Sau đó chọn:

**Include as pending below → Register pending targets**

Target sẽ xuất hiện trong Target Group.

Ban đầu trạng thái có thể là:

Initial

Sau khi ALB thực hiện health check, trạng thái sẽ chuyển thành:

Healthy

nếu backend phản hồi đúng.


#### 4.5.2.5. Tạo Application Load Balancer

Vào:

**EC2 → Load Balancers → Create Load Balancer**

Chọn:

Application Load Balancer

Đặt tên:

knoverse-backend-alb

#### 4.5.2.6. Cấu hình Scheme

Chọn:

Scheme: Internet-facing

Điều này cho phép ALB nhận traffic từ bên ngoài VPC.

Đây là configuration phù hợp với kiến trúc hiện tại vì CloudFront cần truy cập được ALB origin.

IP address type:

IPv4

#### 4.5.2.7. Chọn VPC và Availability Zones

Chọn VPC của KnoVerse:

vpc-0a94136df6e8c9a03

Chọn ít nhất hai Availability Zones.

Ví dụ:

ap-southeast-1c

ap-southeast-1a

với các subnet tương ứng.

Việc sử dụng nhiều Availability Zones giúp ALB có khả năng hoạt động ổn định hơn nếu một Availability Zone gặp sự cố.


