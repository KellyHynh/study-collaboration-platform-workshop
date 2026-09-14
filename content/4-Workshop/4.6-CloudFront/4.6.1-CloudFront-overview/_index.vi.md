---

title: "Tổng quan về Amazon CloudFront"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.6.1. </b> "

---

# Tổng quan về Amazon CloudFront

#### 4.6.1.1. Vai trò trong kiến trúc KnoVerse

CloudFront nằm ở lớp ngoài cùng của backend architecture.

![ALB as CloudFront Origin](/images/4-Workshop/4.6-CloudFront/1.png)

CloudFront cung cấp một public endpoint cho backend:

https://<cloudfront-domain>

Ví dụ trong KnoVerse:

https://d2hvns14tchtf3.cloudfront.net

API có thể được truy cập thông qua:

https://d2hvns14tchtf3.cloudfront.net/api/courses

#### 4.6.1.2. Mục đích sử dụng

CloudFront được sử dụng để:

- Cung cấp endpoint public cho application.
- Đứng trước ALB trong kiến trúc backend.
- Hỗ trợ HTTPS cho client connection.
- Phân phối request thông qua AWS edge network.
- Tạo lớp trung gian giữa client và origin.
- Cho phép áp dụng các chính sách bảo mật và caching.
- Có thể tích hợp AWS WAF để kiểm soát request.

Trong KnoVerse, CloudFront không trực tiếp truy cập EC2. Request được chuyển đến ALB, sau đó ALB mới forward request đến backend.

#### 4.6.1.3. Lý do lựa chọn CloudFront

CloudFront phù hợp với kiến trúc KnoVerse vì hệ thống cần một public endpoint có thể được truy cập từ nhiều network khác nhau.

CloudFront cũng cho phép mở rộng kiến trúc về sau để phục vụ:

- Static assets.
- API.
- Frontend content.
- Cached resources.
- HTTPS traffic.
- WAF protection.

Đối với workshop, việc sử dụng CloudFront giúp minh họa cách một AWS CDN/distribution được tích hợp với backend application đang chạy trên EC2 thông qua ALB.

