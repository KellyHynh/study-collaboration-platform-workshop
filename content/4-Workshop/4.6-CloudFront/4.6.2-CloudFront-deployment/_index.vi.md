---

title: "Triển khai Amazon CloudFront"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.6.2. </b> "

---

# Triển khai Amazon CloudFront

Phần này trình bày toàn bộ quy trình triển khai CloudFront theo trình tự thực hiện thực tế. CloudFront sử dụng Application Load Balancer làm origin, vì vậy quá trình triển khai kiểm tra kết nối CloudFront -> ALB -> EC2 -> RDS.

#### 4.6.2.1. Chuẩn bị Origin

Trước khi tạo CloudFront distribution, cần đảm bảo ALB đã hoạt động bình thường.

Kiểm tra trực tiếp ALB:

curl.exe -v http://<ALB-DNS>/api/courses

Kết quả mong đợi:

HTTP/1.1 200 OK

Response cần chứa course data. Nếu ALB chưa trả về 200 OK, không nên tiếp tục troubleshooting CloudFront.

#### 4.6.2.2. Tạo CloudFront Distribution

Mở:

AWS Console -> CloudFront -> Distributions -> Create distribution

Đặt distribution name phù hợp, ví dụ:

knoverse-backend-api

#### 4.6.2.3. Cấu hình Origin

Tại phần Origin, nhập DNS name của ALB.

Ví dụ:

knoverse-backend-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com
![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/2.png)
Không sử dụng EC2 public IP làm CloudFront origin. ALB là origin trung gian để quản lý traffic đến backend.

#### 4.6.2.4. Cấu hình Origin Protocol

Origin hiện tại của KnoVerse sử dụng:

HTTP
![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/3.png)

CloudFront sử dụng HTTP để kết nối đến ALB trong khi HTTPS giữa client và CloudFront vẫn được duy trì.

#### 4.6.2.5. Cấu hình Viewer Protocol Policy

Trong Behavior, đặt:

Viewer protocol policy:
Redirect HTTP to HTTPS

API endpoint chính thức là:

https://d2hvns14tchtf3.cloudfront.net/api/courses

#### 4.6.2.6. Cấu hình Allowed HTTP Methods

Cấu hình hiện tại cho phép:

GET
HEAD
POST
PUT
PATCH
DELETE
OPTIONS

Các method này cho phép CloudFront forward các CRUD request của backend đến ALB.

#### 4.6.2.7. Cấu hình Cache Policy

Backend API của KnoVerse sử dụng:

Managed-CachingDisabled

Cấu hình này chuyển request đến backend thay vì trả về dữ liệu cũ từ CloudFront cache. Việc cache không phù hợp với các CRUD mutation API hiện tại.

Kiến trúc hiện tại ưu tiên:

Client
  ↓
CloudFront
  ↓
ALB
  ↓
Backend

#### 4.6.2.8. Cấu hình CloudFront Behavior

Behavior mặc định:

Path pattern:
Default (*)
Origin:
knoverse-backend-alb
Viewer protocol:
Redirect HTTP to HTTPS
Allowed methods:
GET, HEAD, POST, OPTIONS, PUT, PATCH, DELETE
Cache policy:
Managed-CachingDisabled

Implementation hiện tại không sử dụng CloudFront Functions hoặc Lambda@Edge.

#### 4.6.2.9. Cấu hình HTTPS

Sau khi deployment, CloudFront cung cấp:

https://d2hvns14tchtf3.cloudfront.net

Client có thể sử dụng endpoint này thay vì EC2 public address.

#### 4.6.2.10. Deploy Distribution

Tạo distribution sau khi hoàn tất configuration. Chờ deployment hoàn tất trước khi đánh giá endpoint vì configuration có thể chưa được áp dụng ngay tại tất cả edge locations.

#### 4.6.2.11. Kiểm thử CloudFront Endpoint

Sau khi deployment, kiểm tra:

curl.exe -v https://d2hvns14tchtf3.cloudfront.net/api/courses

Kết quả mong đợi:

HTTP/1.1 200 OK

Response body chứa course data. Flow end-to-end là:

CloudFront
    ↓
ALB
    ↓
EC2
    ↓
Backend
    ↓
RDS

#### 4.6.2.12. Kiểm thử từ mạng bên ngoài

Kiểm thử CloudFront URL từ máy tính khác, điện thoại, network khác hoặc mobile data:

https://d2hvns14tchtf3.cloudfront.net/api/courses

Response thành công từ network khác chứng minh application đã được expose thông qua AWS infrastructure thay vì chỉ chạy ở local.

#### 4.6.2.13. Tích hợp với Frontend

Frontend KnoVerse được deploy riêng trên AWS Amplify và sử dụng CloudFront endpoint làm backend API endpoint.
![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/image.png)
Frontend có thể gọi:

GET https://d2hvns14tchtf3.cloudfront.net/api/courses

thay vì:

GET http://localhost:3000/api/courses

