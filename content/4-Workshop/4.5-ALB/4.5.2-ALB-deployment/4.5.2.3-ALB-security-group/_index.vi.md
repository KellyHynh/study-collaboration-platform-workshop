---
title: "ALB API Test and CloudFront Integration"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.5.2.3. </b> "
---

#### 4.5.2.11. Kiểm thử ALB Endpoint

Sau khi target trở thành Healthy, lấy **DNS name** của ALB.

Ví dụ:

knoverse-backend-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com

Kiểm thử:

curl.exe -v [http://<ALB-DNS>/api/courses]

Kết quả mong đợi:

HTTP/1.1 200 OK

Content-Type: application/json

Response phải chứa course data từ KnoVerse.

Đây là bước xác nhận ALB đã thành công trong việc chuyển request đến EC2 backend.


#### 4.5.2.12. Tích hợp ALB với CloudFront

Sau khi ALB hoạt động ổn định, ALB được sử dụng làm **origin** cho CloudFront distribution knoverse-backend-api.

![ALB as CloudFront Origin](images/4-Workshop/4.5-ALB/image.png)

Trong CloudFront, origin được cấu hình trỏ đến ALB DNS:

knoverse-backend-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com

CloudFront sau đó tiếp nhận request từ frontend và chuyển request đến ALB.

#### 4.5.2.13. Kiểm thử API thông qua CloudFront

Sau khi CloudFront distribution hoàn tất deployment, kiểm thử:

curl.exe -v [https://<CLOUDFRONT-DOMAIN>/api/courses]

Ví dụ:

curl.exe -v [https://d2hvns14tchtf3.cloudfront.net/api/courses]

Kết quả mong đợi:

HTTP/1.1 200 OK

và response chứa course data.

Khi bước này thành công, request đã đi qua toàn bộ backend architecture:

CloudFront
    ↓
ALB
    ↓
Target Group
    ↓
EC2
    ↓
Backend
    ↓
RDS


Nếu CloudFront trả về 502 hoặc 504 trong quá trình cấu hình, không nên kết luận EC2 hoặc ALB bị lỗi ngay. Cần kiểm tra riêng từng layer bằng cách gọi trực tiếp ALB trước, sau đó mới kiểm tra CloudFront origin connection.
