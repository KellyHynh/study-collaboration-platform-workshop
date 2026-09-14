---

title: "Kiểm thử CloudFront"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.6.3. </b> "

---

# Kiểm thử CloudFront

#### 4.6.3.1. Kiểm thử theo từng layer

Để troubleshoot CloudFront, kiểm tra theo thứ tự:

Bước 1 - EC2

EC2 -> Backend -> RDS

Kiểm tra backend có trả dữ liệu không.

Bước 2 - ALB

ALB /api/courses

Expected:

200 OK

Bước 3 - CloudFront

CloudFront /api/courses

Expected:

200 OK

Cách tiếp cận này giúp xác định chính xác layer gây lỗi.

#### 4.6.3.2. Kiểm tra CloudFront Metrics

Có thể theo dõi:

- Requests.
- Bytes downloaded.
- Error rate.
- HTTP status.
- Cache behavior.

Các metrics giúp xác định distribution có nhận request hay không và request có được xử lý thành công hay không.

#### 4.6.3.3. Phân tích HTTP Status Code

| **Status** | **Ý nghĩa trong troubleshooting** |
| --- | --- |
| 200 | Request thành công |
| 301/302 | Redirect, thường liên quan HTTP đến HTTPS |
| 403 | Request bị từ chối |
| 502 | CloudFront không nhận được response hợp lệ từ origin |
| 504 | CloudFront không nhận được response từ origin trong thời gian cho phép |

Khi CloudFront trả về 502 hoặc 504, cần kiểm tra origin ALB trước. Nếu ALB cũng lỗi, vấn đề nằm ở ALB, EC2 hoặc backend. Nếu ALB trả về 200 nhưng CloudFront lỗi, tập trung kiểm tra CloudFront origin configuration và connection đến origin.

#### 4.6.3.4. Các vấn đề có thể gặp

**CloudFront trả 502 Bad Gateway**

Kiểm tra:

- Origin DNS.
- Origin protocol.
- Origin port.
- ALB listener.
- Target Group.
- EC2 backend.

**CloudFront trả 504 Gateway Timeout**

Kiểm tra:

- ALB có phản hồi không.
- EC2 có đang chạy không.
- Backend có bị timeout không.
- Target có healthy không.
- Network và Security Group configuration.

**CloudFront trả 403**

Kiểm tra:

- WAF rules.
- CloudFront behavior.
- Allowed methods.
- Origin configuration.
- Request restrictions.

#### 4.6.3.5. Tối ưu caching

API hiện tại sử dụng Managed-CachingDisabled vì dữ liệu thay đổi thường xuyên trong giai đoạn backend CRUD.

Trong tương lai, các resources ít thay đổi như `/static/*` và `/assets/*` có thể được cache trong khi các mutation API tiếp tục bypass cache.

#### 4.6.3.6. AWS WAF Integration

CloudFront có thể tích hợp AWS WAF để bảo vệ application trước các request không mong muốn. Trong KnoVerse, WAF đã được bật trên CloudFront distribution.

WAF có thể được sử dụng để:

- Kiểm soát request.
- Block malicious traffic.
- Rate limit traffic.
- Theo dõi request patterns.
- Bổ sung security layer trước origin.

Flow:

Client
  ↓
CloudFront
  ↓
AWS WAF
  ↓
ALB
  ↓
EC2

WAF nằm ở lớp edge/security và không thay thế Security Groups hoặc các network security mechanisms khác.

#### 4.6.3.7. Kết quả đạt được

Sau khi hoàn thành CloudFront deployment:

- CloudFront distribution `knoverse-backend-api` được tạo.
- ALB được cấu hình làm CloudFront origin.
- Client sử dụng HTTPS để truy cập backend.
- HTTP request được redirect sang HTTPS.
- CloudFront hỗ trợ các HTTP methods cần thiết cho backend CRUD.
- API caching được disabled để request được chuyển đến backend.
- CloudFront chuyển request đến ALB.
- ALB forward request đến EC2.
- EC2 xử lý request và truy vấn RDS.
- `/api/courses` trả về course data thông qua CloudFront.
- AWS WAF được tích hợp ở CloudFront layer.

Endpoint cuối cùng của backend:

https://d2hvns14tchtf3.cloudfront.net/api/courses

![ALB as CloudFront Origin](/images/4-Workshop/4.6-CloudFront/1.png)