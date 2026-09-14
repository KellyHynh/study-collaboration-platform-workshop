---

title: "Kiểm tra S3 Access từ EC2"
date: 2026-09-14
weight: 6
chapter: false
pre: " <b> 4.8.2.6. </b> "

---

# Kiểm tra S3 Access từ EC2

Tích hợp S3 được xác minh từ EC2 instance bằng AWS CLI.

#### Bước 1: Kết nối tới EC2

SSH vào EC2 instance đang chạy KnoVerse backend.

Terminal sẽ hiển thị môi trường EC2, ví dụ:

[ec2-user@ip-172-31-13-175 ~]$

#### Bước 2: Xác minh IAM Identity

Chạy:

aws sts get-caller-identity

Kết quả mong đợi chứa IAM Role:

assumed-role/knoverse-ec2-s3-role

Điều này xác nhận EC2 instance đang sử dụng IAM Role mong đợi.

#### Bước 3: Kiểm tra Bucket Access

Chạy:

aws s3 ls s3://knoverse-assets-2026

Output mong đợi bao gồm:

PRE courses/

#### Bước 4: Kiểm tra Object Access

Chạy:

aws s3 ls s3://knoverse-assets-2026/courses/thumbnails/

Output mong đợi bao gồm object đã upload:

course-react.png

Kiểm thử thành công chứng minh luồng truy cập sau:

EC2
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3 Bucket
 ↓
courses/thumbnails/course-react.png

Trong lần kiểm thử ban đầu, permission s3:ListBucket bị thiếu, khiến lệnh aws s3 ls trên bucket trả về lỗi AccessDenied. Sau đó policy được cập nhật để bổ sung rõ ràng s3:ListBucket ở bucket level. Sau khi cập nhật, các lệnh liệt kê bucket và object đã hoàn tất thành công.

Bước troubleshooting này xác nhận IAM permissions đã được kiểm thử bằng operation EC2-to-S3 thực tế thay vì chỉ được cấu hình trong AWS Console.

Evidence 4.8.2.6: Screenshot của EC2 terminal hiển thị các AWS CLI commands với kết quả thành công.

