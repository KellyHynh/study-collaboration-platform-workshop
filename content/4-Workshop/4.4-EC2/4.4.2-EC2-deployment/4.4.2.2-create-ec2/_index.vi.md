---

title: "Tạo EC2 Instance"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.4.2.2. </b> "

---

Phần này trình bày quy trình tạo EC2 instance để chạy backend application của KnoVerse.

#### Bước 1 — Mở Amazon EC2

Trong AWS Management Console, truy cập:

Services → EC2 → Instances → Launch instance

Đảm bảo Region được chọn là:

ap-southeast-1

![Mở Amazon EC2](images/4-Workshop/4.4-EC2/3.png)

#### Bước 2 — Đặt tên Instance

Đặt tên để dễ dàng nhận diện instance.

Ví dụ:

knoversee-backend

#### Bước 3 — Chọn Operating System

Chọn một Amazon Machine Image (AMI) phù hợp với backend application.

Trong workshop này có thể sử dụng Amazon Linux.

#### Bước 4 — Chọn Instance Type

Chọn instance type phù hợp với workload của project và AWS Free Tier hoặc credits hiện có.

Đối với môi trường development hoặc demo, nên ưu tiên instance nhỏ để giảm chi phí.

#### Bước 5 — Tạo Key Pair

Tạo hoặc chọn EC2 Key Pair để sử dụng khi kết nối đến instance thông qua SSH.

Private key phải được lưu trữ an toàn.

Không commit file private key vào Git repository.

#### Bước 6 — Cấu hình Network Settings

Chọn:

- KnoVerse VPC.

- Subnet phù hợp.

- Public IP configuration phù hợp với cách truy cập EC2 instance.

Security Group sẽ được cấu hình riêng để cho phép các traffic cần thiết.

#### Bước 7 — Launch Instance

Kiểm tra lại configuration và chọn:

**Launch instance**

Chờ instance chuyển sang trạng thái **Running** và các system status checks hoàn tất.

![EC2 Network Settings](images/4-Workshop/4.4-EC2/4.png)

