---

title: "Tạo IAM Policy"
date: 2026-09-14
weight: 4
chapter: false
pre: " <b> 4.8.2.4. </b> "

---

# Tạo IAM Policy

S3 bucket không nên được backend EC2 truy cập bằng AWS access keys được hard-code. Thay vào đó, backend sử dụng IAM Role.

Các permissions cần thiết được giới hạn ở:

s3:ListBucket
s3:GetObject
s3:PutObject
s3:DeleteObject

#### Bước 1: Mở IAM

Đi tới:

AWS Console
→ IAM
→ Roles
→ Create role

#### Bước 2: Chọn Trusted Entity

Tại Trusted entity type, chọn:

AWS service

Tại service/use case, chọn:

EC2

Cấu hình này tạo trust relationship cho phép EC2 instances assume role.

Trust relationship sau khi tạo bao gồm:

{
  "Effect": "Allow",
  "Action": "sts:AssumeRole",
  "Principal": {
    "Service": "ec2.amazonaws.com"
  }
}

#### Bước 3: Tạo Permission Policy

Tạo một inline policy cho role. Policy tách bucket-level permissions và object-level permissions vì s3:ListBucket áp dụng cho chính bucket, trong khi các object operations áp dụng cho các object bên trong bucket.

Policy được sử dụng là:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "KnoVerseS3BucketAccess",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::knoverse-assets-2026"
    },
    {
      "Sid": "KnoVerseS3ObjectAccess",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::knoverse-assets-2026/*"
    }
  ]
}

Statement đầu tiên cấp quyền truy cập vào bucket:

arn:aws:s3:::knoverse-assets-2026

Statement thứ hai cấp quyền truy cập vào các object bên trong bucket:

arn:aws:s3:::knoverse-assets-2026/*

Cách này tránh cấp quyền S3 không giới hạn như:

s3:*

#### Bước 4: Đặt tên Role

IAM Role có tên:

knoverse-ec2-s3-role

Mô tả:

IAM role cho backend EC2 truy cập KnoVerse S3 assets.

#### Bước 5: Tạo Role

Kiểm tra:

- Trusted entity: EC2
- S3 permissions: giới hạn trong knoverse-assets-2026
- Role name: knoverse-ec2-s3-role

Sau đó chọn Create role.

Evidence 4.8.2.4: Screenshot hiển thị IAM Role, EC2 trusted entity và S3 permissions.

