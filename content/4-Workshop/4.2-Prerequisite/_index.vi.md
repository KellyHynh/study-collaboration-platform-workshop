---

title: "Prerequisite"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.2. </b> "

---

# Điều kiện tiên quyết

Trước khi bắt đầu triển khai KnoVerse trên AWS, cần chuẩn bị tài khoản cloud, môi trường phát triển, mã nguồn ứng dụng, cấu hình cơ sở dữ liệu và các quyền truy cập cần thiết. Các điều kiện dưới đây xác định môi trường được sử dụng xuyên suốt workshop triển khai KnoVerse.

## 4.2.1. Tài khoản AWS và thanh toán

Cần có một tài khoản AWS đang hoạt động để tạo và cấu hình các tài nguyên cloud được sử dụng trong workshop.

Tài khoản AWS cần có:

* Quyền truy cập AWS Management Console.
* Quyền tạo và cấu hình các tài nguyên AWS cần thiết.
* Cấu hình thanh toán hợp lệ hoặc AWS credits phù hợp.
* Quyền sử dụng AWS Free Tier nếu tài khoản đủ điều kiện.

Một số tài nguyên AWS có thể phát sinh chi phí trong thời gian hoạt động, vì vậy cần theo dõi billing và mức sử dụng tài nguyên trong suốt quá trình triển khai. Các tài nguyên không còn cần thiết nên được dừng hoặc xóa sau khi hoàn thành workshop để tránh phát sinh chi phí không cần thiết.

## 4.2.2. AWS Region

Tất cả các tài nguyên AWS chính được sử dụng trong quá trình triển khai KnoVerse đều được tạo trong AWS Region sau:

**Region:** `ap-southeast-1`

**Tên Region:** Asia Pacific (Singapore)

Việc sử dụng thống nhất một Region giúp đơn giản hóa việc quản lý tài nguyên và kết nối mạng giữa các dịch vụ như Amazon EC2, Amazon RDS và Application Load Balancer.

Cần xác nhận Region trước khi tạo tài nguyên vì một số tài nguyên và cấu hình AWS phụ thuộc vào từng Region.

## 4.2.3. Quyền truy cập IAM

Cần sử dụng một AWS identity có đủ quyền để tạo, cấu hình và quản lý các tài nguyên được sử dụng trong workshop.

Các quyền truy cập cần thiết bao gồm những dịch vụ và nhóm tài nguyên AWS sau:

* Amazon EC2
* Amazon RDS
* Amazon VPC
* Elastic Load Balancing
* Amazon CloudFront
* AWS WAF
* Amazon S3
* AWS Amplify
* AWS Identity and Access Management (IAM), khi cần thiết để cấu hình các dịch vụ.

Trong phạm vi học tập và workshop, có thể sử dụng tài khoản có quyền quản trị rộng để đơn giản hóa quá trình tạo tài nguyên. Trong môi trường production, quyền truy cập nên tuân theo **nguyên tắc đặc quyền tối thiểu (principle of least privilege)**, chỉ cấp những quyền cần thiết cho từng thao tác.

Không nên sử dụng AWS root account cho các hoạt động triển khai thường xuyên.

## 4.2.4. Môi trường phát triển

Môi trường phát triển local cần cung cấp các công cụ cần thiết để chuẩn bị, kiểm thử và triển khai ứng dụng KnoVerse.

### Các công cụ cần thiết

* Git
* Node.js
* npm
* Visual Studio Code hoặc một trình soạn thảo mã nguồn khác.
* Web browser
* Terminal hoặc PowerShell

### Công cụ AWS

* AWS Management Console
* AWS CLI

AWS Management Console được sử dụng để cấu hình và theo dõi các tài nguyên AWS trong suốt workshop, trong khi AWS CLI có thể được sử dụng để kiểm tra và quản lý tài nguyên thông qua command line.

## 4.2.5. Mã nguồn ứng dụng

Mã nguồn KnoVerse cần được chuẩn bị trước khi bắt đầu quá trình triển khai.

Ứng dụng bao gồm hai thành phần chính:

```text
KnoVerse
├── Frontend
└── Backend
```

Frontend cần có khả năng build thành công trong môi trường phát triển local và giao tiếp được với backend API.

Backend cần có khả năng:

* Chạy trên Node.js.
* Cung cấp các REST API endpoint cần thiết.
* Kết nối với PostgreSQL database.
* Nhận các cấu hình theo từng môi trường thông qua environment variables.
* Chạy thành công trong môi trường local trước khi triển khai.

Các chức năng của ứng dụng nên được kiểm tra trước khi đưa vào infrastructure AWS. Điều này giúp phân biệt được các vấn đề phát sinh từ quá trình deployment với các vấn đề bên trong ứng dụng.

## 4.2.6. Điều kiện tiên quyết về Database

Trước khi triển khai Amazon RDS, cấu trúc database và các cấu hình cần thiết phải được chuẩn bị.

Các thành phần cần có:

* PostgreSQL database schema.
* Các bảng và mối quan hệ cần thiết.
* Database migrations hoặc initialization scripts.
* Seed hoặc dữ liệu mẫu nếu cần.
* Database credentials.
* Cấu hình kết nối database cho backend.

Thông tin kết nối database nên được cung cấp thông qua environment variables thay vì hard-code trực tiếp vào source code.

Các biến môi trường thường bao gồm:

```text
DB_HOST
DB_PORT
DB_NAME
DB_USER
DB_PASSWORD
```

Các thông tin nhạy cảm như database credentials không được commit vào source code repository.

## 4.2.7. Điều kiện tiên quyết về Network

Quá trình triển khai AWS yêu cầu một môi trường network có khả năng hỗ trợ kết nối giữa các thành phần public-facing, backend application và database.

Hệ thống sử dụng các thành phần network sau:

* Amazon VPC
* Subnets
* Route Tables
* Internet Gateway
* Security Groups
* Network ACL
* Application Load Balancer

Các thành phần này cung cấp khả năng kết nối mạng và kiểm soát traffic cần thiết cho kiến trúc KnoVerse.

Cấu hình chi tiết cũng như mối quan hệ giữa các thành phần này sẽ được trình bày trong các phần networking và deployment tiếp theo của workshop.

## 4.2.8. Cấu hình AWS CLI

AWS CLI là công cụ tùy chọn trong quá trình deployment nếu các tài nguyên được cấu hình thông qua AWS Management Console. Tuy nhiên, AWS CLI có thể được sử dụng để xác minh AWS account và thực hiện các thao tác thông qua command line.

Sau khi cài đặt, có thể kiểm tra cấu hình AWS CLI bằng lệnh:

```bash
aws sts get-caller-identity
```

Lệnh này xác nhận AWS identity hiện đang được sử dụng bởi AWS CLI và giúp tránh thực hiện các thao tác deployment trên nhầm AWS account.

## 4.2.9. Công cụ Infrastructure-as-Code

Các công cụ Infrastructure-as-Code như **AWS SAM, AWS CDK và Terraform** không bắt buộc trong workshop này.

Quá trình triển khai KnoVerse tập trung vào việc tìm hiểu và triển khai AWS infrastructure thông qua AWS Management Console, kết hợp với các công cụ command line khi cần thiết để kiểm tra.

Các công cụ Infrastructure-as-Code được đề cập như những lựa chọn tùy chọn cho việc tự động hóa và tái tạo infrastructure trong tương lai.

## 4.2.10. Nhận thức về chi phí AWS

Trước khi tạo các AWS resources, cần xem xét chi phí có thể phát sinh từ infrastructure được triển khai.

Workshop sử dụng một số AWS services có thể phát sinh chi phí tùy thuộc vào điều kiện tài khoản, cấu hình resource và mức độ sử dụng. Vì vậy, nên thực hiện các biện pháp sau:

* Kiểm tra AWS Free Tier hoặc AWS credits nếu áp dụng.
* Theo dõi thông tin billing trong quá trình deployment.
* Tránh duy trì các resource không cần thiết sau khi kiểm thử.
* Stop hoặc delete các resource không còn sử dụng.
* Kiểm tra lại toàn bộ resource đã triển khai trước khi kết thúc workshop.

Việc theo dõi chi phí đặc biệt quan trọng đối với các tài nguyên liên quan đến compute, database, load balancing, networking và các AWS services có tính phí dựa trên mức sử dụng.


