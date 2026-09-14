---
title: "Application Load Balancer Overview"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.5.1. </b> "
---

#### 4.5.1.1. Vai trò trong kiến trúc KnoVerse

ALB nằm giữa CloudFront và EC2.

![KnoVerse ALB Architecture](/images/4-Workshop/4.5-ALB/1.png)

Khi client gửi request đến API, request được chuyển đến ALB. ALB sau đó chuyển tiếp request đến target phù hợp trong Target Group.

Với endpoint:

GET /api/courses

flow xử lý là:

GET /api/courses
        │
        ▼
CloudFront
        │
        ▼
ALB :80
        │
        ▼
Target Group
        │
        ▼
EC2 :3000
        │
        ▼
Express Backend
        │
        ▼
RDS PostgreSQL

#### 4.5.1.2. Mục đích sử dụng ALB

ALB được sử dụng nhằm:

- Cung cấp một endpoint ổn định cho backend.
- Không yêu cầu client truy cập trực tiếp EC2.
- Định tuyến HTTP request đến backend.
- Kiểm tra trạng thái của EC2 thông qua health check.
- Làm origin cho CloudFront.
- Cho phép kiến trúc có thể mở rộng thêm nhiều EC2 instance trong tương lai.

Việc sử dụng ALB cũng giúp tách biệt public access layer khỏi application server layer.

#### 4.5.1.3. Lý do lựa chọn ALB

ALB phù hợp với KnoVerse vì backend sử dụng HTTP/REST API và cần một thành phần có khả năng định tuyến Layer 7.

ALB hỗ trợ:

- HTTP/HTTPS.
- Path-based routing.
- Target Groups.
- Health Checks.
- Integration với EC2.
- Integration với CloudFront.
- Khả năng mở rộng nhiều backend instances.

Đối với project hiện tại, ALB chủ yếu được sử dụng để định tuyến request đến EC2 và làm origin cho CloudFront.
