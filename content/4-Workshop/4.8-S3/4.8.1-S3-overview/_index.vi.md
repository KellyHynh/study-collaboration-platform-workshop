---

title: "Tổng quan về Amazon S3"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.8.1. </b> "

---

# Tổng quan về Amazon S3

#### 4.8.1.1. Vai trò của Amazon S3

Amazon S3 (Simple Storage Service) được sử dụng trong KnoVerse như một dịch vụ lưu trữ đối tượng để lưu trữ các file được upload và các tài nguyên của ứng dụng.

Hệ thống tách biệt dữ liệu ứng dụng có cấu trúc khỏi dữ liệu dạng file.
![ALB as CloudFront Origin](/images/4-Workshop/4.8-S3/1.png)

Amazon RDS PostgreSQL chịu trách nhiệm lưu trữ dữ liệu quan hệ có cấu trúc như thông tin khóa học, bài học, quiz, câu hỏi và metadata liên quan. Amazon S3 được sử dụng để lưu trữ các file và object như course thumbnail.

Ví dụ, thay vì lưu trực tiếp binary image bên trong PostgreSQL, database có thể lưu object key:

thumbnailKey =
courses/thumbnails/course-react.png

trong khi image thực tế được lưu trong S3. Sự phân tách này giúp kiến trúc lưu trữ phù hợp hơn với từng loại dữ liệu và cho phép mở rộng object storage layer trong tương lai.

#### 4.8.1.2. Use Case của S3 trong KnoVerse

Use case ban đầu của S3 là lưu trữ course assets, cụ thể là course thumbnails.

Cấu trúc object ban đầu là:

knoverse-assets-2026/
└── courses/
    └── thumbnails/
        └── course-react.png

Cấu trúc này có thể được mở rộng trong tương lai để hỗ trợ các tài nguyên được upload khác:

knoverse-assets-2026/
├── courses/
│   └── thumbnails/
├── lessons/
├── materials/
└── users/

Ở giai đoạn triển khai hiện tại, mục tiêu là thiết lập hạ tầng S3, cấu hình quyền truy cập an toàn và xác minh backend trên EC2 có thể truy cập bucket thông qua IAM Role.


