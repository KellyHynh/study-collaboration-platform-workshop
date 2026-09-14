---

title: "Tổng quan về Amazon RDS"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.3.1. </b> "

---

# Tổng quan về Amazon RDS

#### 4.3.1.1. Mục đích sử dụng Amazon RDS

Amazon Relational Database Service (Amazon RDS) được sử dụng trong KnoVerse để cung cấp môi trường cơ sở dữ liệu PostgreSQL được quản lý trên AWS.

Trong giai đoạn phát triển ban đầu, backend của KnoVerse sử dụng PostgreSQL trên máy tính local. Khi triển khai hệ thống lên AWS, cơ sở dữ liệu được chuyển sang Amazon RDS để ứng dụng backend chạy trên Amazon EC2 có thể truy cập cơ sở dữ liệu thông qua mạng AWS.

Các mục tiêu chính khi triển khai Amazon RDS bao gồm:

- Chuyển cơ sở dữ liệu KnoVerse lên môi trường cloud.

- Tách cơ sở dữ liệu khỏi application server.

- Cho phép backend chạy trên EC2 truy cập cơ sở dữ liệu thông qua private network.

- Duy trì cấu trúc dữ liệu và database schema hiện có của ứng dụng.

- Cung cấp nền tảng để quản lý và mở rộng cơ sở dữ liệu trong môi trường AWS.

#### 4.3.1.2. Tại sao chọn Amazon RDS?

Amazon RDS được lựa chọn thay vì cài đặt và quản lý PostgreSQL trực tiếp trên một EC2 instance.

Các lý do chính bao gồm:

**Managed service:** AWS quản lý nhiều tác vụ liên quan đến hạ tầng cơ sở dữ liệu, giúp giảm lượng công việc quản trị cơ sở dữ liệu thủ công cần thực hiện.

**AWS integration:** Amazon RDS hoạt động trong Amazon VPC và có thể giao tiếp với các tài nguyên AWS khác thông qua cấu hình mạng và bảo mật phù hợp.

**PostgreSQL support:** KnoVerse sử dụng PostgreSQL làm database engine, do đó Amazon RDS for PostgreSQL tương thích với môi trường cơ sở dữ liệu hiện có của ứng dụng.

**Application and database separation:** Backend có thể chạy trên EC2 trong khi cơ sở dữ liệu được quản lý riêng bởi RDS. Điều này tạo ra sự phân tách rõ ràng giữa application layer và database layer.

**Scalability:** Amazon RDS cung cấp các tùy chọn để thay đổi compute capacity, storage và database configurations khi hệ thống phát triển trong tương lai.

#### 4.3.1.3. Vai trò trong kiến trúc KnoVerse

Sau khi hạ tầng AWS được triển khai, Amazon RDS chịu trách nhiệm cho **database layer** của hệ thống KnoVerse.

Kiến trúc kết nối chính được minh họa bên dưới:

![KnoVerse RDS Architecture](images/4-Workshop/4.3-RDS/image1.png)

Backend không truy cập cơ sở dữ liệu thông qua CloudFront hoặc Application Load Balancer. Các request từ client trước tiên được xử lý bởi backend application chạy trên EC2. Sau đó, backend thực hiện các thao tác với cơ sở dữ liệu Amazon RDS thông qua AWS network đã được cấu hình.

Sự phân tách này cho phép application layer và database layer được quản lý độc lập trong khi vẫn duy trì việc giao tiếp có kiểm soát giữa hai thành phần.


