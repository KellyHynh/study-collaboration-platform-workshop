---

title: "Gắn IAM Role vào EC2"
date: 2026-09-14
weight: 5
chapter: false
pre: " <b> 4.8.2.5. </b> "

---

# Gắn IAM Role vào EC2

Sau khi tạo IAM Role, role này phải được gắn vào EC2 instance đang chạy KnoVerse backend.

#### Bước 1: Mở EC2

Đi tới:

AWS Console
→ EC2
→ Instances

Chọn EC2 instance đang chạy KnoVerse backend.

#### Bước 2: Chỉnh sửa IAM Role

Chọn:

Actions
→ Security
→ Modify IAM role

#### Bước 3: Chọn Role

Tại IAM Role, chọn:

knoverse-ec2-s3-role

Sau đó nhấn Update IAM role.

Luồng truy cập sau khi cấu hình là:

EC2
  ↓
knoverse-ec2-s3-role
  ↓
IAM Policy
  ↓
knoverse-assets-2026

Điều này cho phép backend EC2 lấy AWS credentials thông qua IAM Role mà không cần lưu long-term AWS credentials trong source code của ứng dụng.

Evidence 4.8.2.5: Screenshot của EC2 instance hiển thị knoverse-ec2-s3-role đã được gắn.

