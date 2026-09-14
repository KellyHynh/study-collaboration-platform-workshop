---

title: "Tích hợp EC2 với Application Load Balancer"

date: 2026-09-14

weight: 11

chapter: false

pre: " <b> 4.4.2.11. </b> "

---

Sau khi backend hoạt động ổn định trên EC2, instance được đưa vào Target Group của Application Load Balancer.

Luồng traffic:

Client

 │

 ▼

Application Load Balancer

 │

 ▼

Target Group

 │

 ▼

EC2 :3000

Target Group cần được cấu hình với:

Protocol: HTTP

Port: 3000

Health check sử dụng endpoint phù hợp để xác định backend có hoạt động hay không.

Sau khi EC2 được đăng ký vào Target Group, kiểm tra target health.

Trạng thái mong đợi:

Healthy

![EC2 Target Group](/images/4-Workshop/4.4-EC2/10.png)

