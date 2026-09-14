---

title: "Tạo Object Structure"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 4.8.2.2. </b> "

---

# Tạo Object Structure

Sau khi tạo bucket, tạo object structure để tổ chức các course assets.

#### Bước 1: Mở Bucket

Đi tới:

S3 → Buckets → knoverse-assets-2026

#### Bước 2: Tạo Courses Prefix

Nhấn Create folder và tạo:

courses/

#### Bước 3: Tạo Thumbnails Prefix

Mở thư mục courses/ và tạo:

thumbnails/

Cấu trúc tạo được là:

knoverse-assets-2026/
└── courses/
    └── thumbnails/

Mặc dù S3 console hiển thị chúng dưới dạng folder, S3 lưu object bằng keys và prefixes. Vì vậy, cấu trúc này cung cấp cách tổ chức logic cho các object được upload.

Evidence 4.8.2.2: Screenshot hiển thị cấu trúc courses/thumbnails/.

