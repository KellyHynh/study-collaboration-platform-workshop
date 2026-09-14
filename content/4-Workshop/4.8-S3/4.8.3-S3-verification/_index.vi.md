---

title: "Kiểm thử S3"

date: 2026-09-14

weight: 4

chapter: false

pre: " <b> 4.8.3. </b> "

---

# Kiểm thử S3

Sau khi hoàn thành triển khai Amazon S3, bucket, object access, IAM Role và kết nối EC2-to-S3 cần được kiểm thử và đánh giá.

#### 4.8.3.1. Kiểm thử

Triển khai S3 được kiểm thử ở nhiều cấp độ:

| **Test** | **Mục đích** | **Kết quả** |
| --- | --- | --- |
| Bucket creation | Xác minh S3 resource | Đạt |
| Object upload | Xác minh object storage | Đạt |
| aws sts get-caller-identity | Xác minh EC2 IAM Role | Đạt |
| aws s3 ls | Xác minh bucket access | Đạt |
| Object listing | Xác minh object access | Đạt |

Kiểm thử cuối cùng xác nhận môi trường backend EC2 có thể truy cập KnoVerse S3 bucket bằng IAM Role đã gắn.

#### 4.8.3.2. Các lưu ý về Security

S3 bucket sử dụng Block Public Access, ngăn truy cập public trực tiếp tới bucket và các object của bucket.

Quyền truy cập từ EC2 được kiểm soát thông qua:

EC2
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3

Policy tuân theo nguyên tắc least privilege bằng cách chỉ cấp các S3 operations cần thiết và giới hạn quyền truy cập trong KnoVerse bucket.

Long-term AWS access keys và secret keys không được hard-code vào backend source code.

#### 4.8.3.3. Kết quả

Amazon S3 đã được thêm thành công vào kiến trúc KnoVerse với vai trò object-storage layer. Triển khai hiện tại thiết lập và xác minh infrastructure truy cập EC2-to-S3. Xử lý upload ở application level thông qua backend vẫn là phần có thể mở rộng trong tương lai.

Triển khai đã thành công minh họa:

1. Tạo một S3 bucket riêng cho hệ thống.
2. Cấu hình private bucket access.
3. Tổ chức course assets bằng S3 prefixes.
4. Upload một course thumbnail object.
5. Tạo IAM Role dành riêng cho EC2.
6. Cấu hình S3 permissions ở mức giới hạn.
7. Gắn IAM Role vào EC2 backend instance.
8. Xác minh IAM identity từ EC2 thành công.
9. Truy cập S3 bucket và object đã upload từ EC2 thành công.

S3 bổ sung cho RDS thay vì thay thế RDS: RDS lưu trữ dữ liệu ứng dụng có cấu trúc, trong khi S3 lưu trữ các object và asset dạng file.

![ALB as CloudFront Origin](images/4-Workshop/4.8-S3/1.png)