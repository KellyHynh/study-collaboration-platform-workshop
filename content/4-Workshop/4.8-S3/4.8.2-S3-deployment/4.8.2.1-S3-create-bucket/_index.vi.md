---

title: "Tạo S3 Bucket"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.8.2.1. </b> "

---

# Tạo S3 Bucket

Bước đầu tiên là tạo một S3 bucket để lưu trữ các asset của KnoVerse.

#### Bước 1: Mở Amazon S3

1. Đăng nhập vào AWS Management Console.
2. Mở Amazon S3.
3. Chọn Buckets từ thanh điều hướng.
4. Nhấn Create bucket.

#### Bước 2: Cấu hình loại Bucket

Tại Bucket type, chọn:

General purpose

General Purpose bucket là đủ cho use case object storage của KnoVerse.

#### Bước 3: Cấu hình tên Bucket

Nhập tên bucket duy nhất trên toàn hệ thống AWS.

Bucket được sử dụng trong triển khai này là:

knoverse-assets-2026

#### Bước 4: Cấu hình Object Ownership

Giữ cấu hình object ownership mặc định:

Bucket owner enforced

Cấu hình này giữ ACL ở trạng thái disabled và cho phép bucket policies cùng IAM permissions kiểm soát quyền truy cập.

#### Bước 5: Cấu hình Public Access

Giữ Block all public access ở trạng thái enabled.

Block Public Access
☑ Block all public access

Bucket không được thiết kế để truy cập trực tiếp từ public Internet. Thay vào đó, quyền truy cập sẽ được kiểm soát thông qua EC2 IAM Role.

#### Bước 6: Cấu hình Encryption

Sử dụng server-side encryption mặc định của Amazon S3:

Server-side encryption:
SSE-S3

Trong triển khai hiện tại, S3 Bucket Key được giữ ở trạng thái disabled vì use case này không yêu cầu cấu hình bổ sung dựa trên KMS.

#### Bước 7: Tạo Bucket

Kiểm tra lại cấu hình và nhấn:

Create bucket

Sau khi tạo, bucket sẽ xuất hiện trong danh sách S3 bucket.

Kết quả mong đợi:

knoverse-assets-2026

Evidence 4.8.2.1: Screenshot của bucket đã tạo và cấu hình của bucket, bao gồm bucket type, Block Public Access và encryption settings.

