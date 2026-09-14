---
title: "Application Load Balancer"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.5. </b> "
---

# Application Load Balancer

Application Load Balancer (ALB) được sử dụng trong kiến trúc KnoVerse để tiếp nhận các HTTP request đến backend và định tuyến request đến EC2 instance đang chạy backend application.

Trong kiến trúc hiện tại, ALB đóng vai trò là điểm truy cập trung gian giữa CloudFront và backend EC2, đồng thời cung cấp cơ chế kiểm tra tình trạng của backend thông qua Target Group và Health Check.

#### Content

1. [ALB Overview](4.5.1-ALB-overview/)

2. [ALB Deployment](4.5.2-ALB-deployment/)

3. [ALB Verification](4.5.3-ALB-verification/)
