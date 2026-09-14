---

title: "Kiểm thử EC2"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.4.3. </b> "

---

#### 4.4.3.1. Kiểm thử Backend Application

Các kiểm thử cơ bản:

| **Test**         | **Expected Result** |
| ---------------- | ------------------- |
| EC2 instance     | Running             |
| Node.js          | Installed           |
| Backend process  | Running             |
| Local API        | 200 OK              |
| RDS connection   | Successful          |
| Database query   | Successful          |
| ALB target       | Healthy             |
| ALB /api/courses | 200 OK              |

Các kiểm thử này xác nhận từng layer trước khi chuyển sang layer tiếp theo.

#### 4.4.3.2. Kiểm thử End-to-End

Sau khi tích hợp EC2 với ALB, kiểm thử toàn bộ backend flow:

HTTP Request

    │

    ▼

    ALB

    │

    ▼

Target Group

    │

    ▼

    EC2

    │

    ▼

KnoVerse Backend

    │

    ▼

    RDS

    │

    ▼

Course Data

Endpoint kiểm thử:

GET /api/courses

Kết quả mong đợi là HTTP 200 OK cùng dữ liệu khóa học.

#### 4.4.3.3. Các vấn đề thường gặp và phương án xử lý

**EC2 không thể SSH**

Kiểm tra:

- Key pair.

- Public IP.

- Security Group port 22.

- Network configuration.

**Backend không start**

Kiểm tra:

- Node.js version.

- Dependencies.

- package.json.

- Environment variables.

- Application logs.

**Backend không kết nối được RDS**

Kiểm tra:

- RDS status.

- RDS endpoint.

- Port 5432.

- RDS Security Group.

- EC2 Security Group.

- Database credentials.

**ALB target Unhealthy**

Kiểm tra:

1. Backend có đang chạy không.

2. Backend có listen đúng port không.

3. Target Group có dùng đúng port không.

4. Health check path có chính xác không.

5. EC2 Security Group có cho phép traffic từ ALB Security Group không.

#### 4.4.3.4. Đánh giá và tối ưu

Sau khi backend hoạt động, EC2 configuration có thể được đánh giá dựa trên:

- CPU utilization.

- Memory usage.

- Network traffic.

- Application response time.

- Instance capacity.

- Application availability.

Khi workload tăng, có thể cân nhắc:

- Thay đổi instance type.

- Sử dụng Auto Scaling.

- Chạy nhiều EC2 instances phía sau ALB.

- Sử dụng process manager để duy trì backend process.

- Theo dõi application và infrastructure metrics bằng Amazon CloudWatch.

Đối với môi trường demo hiện tại, một EC2 instance phía sau ALB là đủ để minh họa architecture và deployment flow.

#### 4.4.3.5. Kết quả đạt được

Sau khi hoàn thành quá trình triển khai:

- Backend KnoVerse được chạy trên Amazon EC2.

- EC2 được đặt trong AWS VPC.

- Security Group kiểm soát traffic đến application.

- Backend kết nối thành công đến Amazon RDS.

- Application Load Balancer phân phối request đến EC2.

- EC2 được Target Group xác nhận ở trạng thái Healthy.

- API /api/courses hoạt động thông qua ALB.

- Backend trở thành application layer của kiến trúc KnoVerse trên AWS.

Kiến trúc sau khi hoàn thành EC2 deployment:

![EC2 Deployment Architecture](/images/4-Workshop/4.4-EC2/1.png)

