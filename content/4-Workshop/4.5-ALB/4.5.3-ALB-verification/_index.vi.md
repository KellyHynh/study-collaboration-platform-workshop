---
title: "ALB Verification"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.5.3. </b> "
---

**#### 4.5.3.1. Kiểm thử theo từng tầng**

Để xác định chính xác vị trí xảy ra lỗi, kiểm thử theo thứ tự:

**Layer 1 — Backend**

EC2 →

localhost:3000/api/courses

Expected:

200 OK

**Layer 2 — ALB**

ALB-DNS/api/courses

Expected:

200 OK

**Layer 3 — CloudFront**

CloudFront-Domain/api/courses

Expected:

200 OK

Cách kiểm thử từng layer giúp tránh việc thay đổi nhiều AWS services cùng lúc khi troubleshooting.

**#### 4.5.3.2. Kiểm tra Health Check**

Target Group cung cấp các trạng thái:

Healthy

Unhealthy

Initial

Draining

Trong deployment hoàn chỉnh, target EC2 cần duy trì trạng thái:

Healthy

Nếu trạng thái thay đổi bất thường, cần kiểm tra application và network configuration.

**#### 4.5.3.3. Đo lường hiệu năng**

Có thể sử dụng các metrics của ALB để theo dõi:

- Request count.
- HTTP response codes.
- Target response time.
- Healthy target count.
- Unhealthy target count.

Các metrics này giúp đánh giá ALB đang xử lý request như thế nào và backend có phản hồi ổn định hay không.

**#### 4.5.3.4. Các vấn đề thường gặp**

**ALB trả về 502 Bad Gateway**

Các nguyên nhân có thể gồm:

- EC2 backend không chạy.
- Backend không listen port 3000.
- Target Group dùng sai port.
- Security Group chặn traffic.
- Application đóng connection hoặc không trả response hợp lệ.

**ALB trả về 503 Service Unavailable**

Thường cần kiểm tra Target Group có target Healthy hay không.

**CloudFront trả về 502/504**

Kiểm tra theo thứ tự:

CloudFront
  ↓
ALB
  ↓
Target Group
  ↓
EC2
  ↓
Backend

Trước tiên phải xác nhận:

ALB /api/courses → 200 OK

Nếu ALB đã trả 200 OK nhưng CloudFront vẫn lỗi, tập trung kiểm tra CloudFront Origin và behavior configuration thay vì tiếp tục thay đổi EC2.

**#### 4.5.3.5. Tối ưu kiến trúc**

Ở workload hiện tại, một EC2 instance là đủ cho mục đích demonstration.

Tuy nhiên, kiến trúc ALB cho phép mở rộng:

ALB
     /       \
    ▼         ▼
  EC2-1     EC2-2
     \       /
      ▼     ▼
         RDS

Trong trường hợp workload tăng, có thể:

- Thêm nhiều EC2 instances.
- Đăng ký nhiều targets vào Target Group.
- Sử dụng Auto Scaling Group.
- Phân phối traffic giữa nhiều instances.
- Sử dụng health check để loại bỏ unhealthy targets.

Điều này giúp kiến trúc có khả năng mở rộng mà không cần thay đổi endpoint mà client sử dụng.

**#### 4.5.3.6. Kết quả đạt được**

Sau khi hoàn thành phần ALB:

- Tạo thành công Application Load Balancer cho KnoVerse.
- ALB được triển khai theo mô hình Internet-facing.
- ALB sử dụng nhiều Availability Zones.
- Target Group được cấu hình cho backend EC2.
- Health Check xác nhận EC2 backend ở trạng thái Healthy.
- Listener HTTP port 80 forward request đến backend Target Group.
- ALB có thể truy cập /api/courses và nhận course data.
- ALB được sử dụng làm origin cho CloudFront.
- Hoàn thành flow backend từ CloudFront → ALB → EC2 → RDS.
