---

title: "Upload Object"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.8.2.3. </b> "

---

# Upload Object

Một course thumbnail mẫu được upload để xác minh bucket có thể lưu trữ asset của KnoVerse.

#### Bước 1: Mở vị trí Thumbnail

Đi tới:

courses/thumbnails/

#### Bước 2: Upload File

Nhấn Upload và chọn một file course thumbnail.

Object kiểm thử được sử dụng trong triển khai này là:

course-react.png

#### Bước 3: Hoàn tất Upload

Nhấn Upload và chờ AWS báo rằng quá trình upload đã hoàn tất thành công.

Object key sau khi upload là:

courses/thumbnails/course-react.png

Cấu trúc cuối cùng là:

knoverse-assets-2026/
└── courses/
    └── thumbnails/
        └── course-react.png

Kết quả mong đợi:

Object course-react.png hiển thị bên trong vị trí courses/thumbnails/.

Evidence 4.8.2.3: Screenshot hiển thị object course-react.png đã được upload thành công.

