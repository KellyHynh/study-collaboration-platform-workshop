---
title: "Test ALB Endpoint and CloudFront Integration"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 4.5.2.2. </b> "
---

#### 4.5.2.8. Cấu hình Security Group cho ALB**

Tạo hoặc sử dụng Security Group dành riêng cho ALB.

Ví dụ:

Security Group:

knoverse-alb-sg

Inbound rule:

Type: HTTP

Protocol: TCP

Port: 80

Source: 0.0.0.0/0

Rule này cho phép HTTP traffic đến ALB.

Outbound traffic có thể được cho phép theo configuration mặc định:

All traffic → 0.0.0.0/0

#### 4.5.2.9. Cấu hình Listener

Listener xác định protocol và port mà ALB sử dụng để nhận request.

Tạo listener:

Protocol: HTTP

Port: 80

Default action:

Forward to:

knoverse-backend-tg

Khi request đến:

[http://<ALB-DNS>/api/courses]

ALB sẽ forward request đến Target Group.

Target Group sau đó chuyển request đến:

EC2:3000

#### 4.5.2.10. Kiểm tra Target Health

Sau khi ALB và Target Group được cấu hình, quay lại:

**Target Groups → knoverse-backend-tg → Targets**

Kiểm tra trạng thái EC2.

Kết quả mong đợi:

Status: Healthy

Nếu target ở trạng thái Unhealthy, cần kiểm tra:

1. Backend có đang chạy không.
2. Backend có listen port 3000 không.
3. Health Check path có chính xác không.
4. EC2 Security Group có cho phép traffic từ ALB Security Group không.
5. Network configuration có chính xác không.
