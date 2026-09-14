---

title: "Lưu ý về Backend Integration"
date: 2026-09-14
weight: 7
chapter: false
pre: " <b> 4.8.2.7. </b> "

---

# Lưu ý về Backend Integration

Triển khai hiện tại thiết lập infrastructure và secure access path giữa EC2 và S3.

Luồng upload hoàn chỉnh ở application level có thể được mở rộng thành:

Frontend
   ↓
Backend API
   ↓
EC2
   ↓
IAM Role
   ↓
S3
   ↓
Uploaded Object

Khi backend thực hiện upload, object có thể được lưu trong S3 trong khi object key tương ứng được lưu trong RDS.

Ví dụ:

File:
course-react.png

S3 object key:
courses/thumbnails/course-react.png

RDS:
thumbnailKey =
courses/thumbnails/course-react.png

Tích hợp upload trực tiếp từ backend không bắt buộc đối với triển khai infrastructure hiện tại. Mục tiêu hiện tại là thiết lập S3, bảo vệ bằng IAM, gắn IAM Role vào EC2 và xác minh EC2 có thể truy cập S3 thành công.

