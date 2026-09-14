---

title: "Kiểm thử Amplify"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.7.3. </b> "

---

# Kiểm thử Amplify

#### 4.7.3.1. Kiểm thử deployment

Sau deployment, thực hiện kiểm tra:

| **Hạng mục** | **Kết quả mong đợi** |
| --- | --- |
| Production URL | Truy cập thành công |
| Frontend rendering | Hiển thị bình thường |
| Static assets | Load thành công |
| API request | Thành công |
| Course data | Hiển thị đúng |
| Backend connection | Hoạt động |
| Database data | Truy xuất thành công |

#### 4.7.3.2. Kiểm thử API communication

Kiểm tra request:

GET /api/courses

Request cần đi qua:

Amplify
   ↓
CloudFront
   ↓
ALB
   ↓
EC2
   ↓
RDS

Backend ALB endpoint đã được xác minh trả về HTTP 200 OK và course data. Production frontend cũng đã hiển thị được course data. Điều này chứng minh pipeline frontend -> backend -> database đã hoạt động end-to-end.

#### 4.7.3.3. Kiểm thử sau khi EC2 restart

Node.js backend ban đầu được chạy trực tiếp bằng:

node src/server.js

Process này phụ thuộc vào terminal hoặc SSH session. Khi terminal đóng, Node.js process có thể dừng:

Node.js stopped
      ↓
ALB health check failed
      ↓
Target = unhealthy
      ↓
CloudFront API request failed
      ↓
Frontend không tải được course data

Backend sau đó được cấu hình sử dụng PM2 để quản lý process.

Mục tiêu:

EC2
 ↓
PM2
 ↓
Node.js Backend
 ↓
ALB

PM2 giúp backend tiếp tục hoạt động khi SSH session đóng và có thể được cấu hình để tự khởi động lại process khi EC2 reboot.

#### 4.7.3.4. Đánh giá kết quả

Sau khi hoàn thành deployment, Amazon Amplify đã đáp ứng vai trò frontend hosting của KnoVerse.

Kết quả đạt được:

- Frontend được deploy thành công lên AWS.
- Production URL có thể truy cập từ Internet.
- Frontend hiển thị đúng giao diện.
- Frontend có thể gọi backend production.
- Course data được lấy thành công từ hệ thống backend.
- Amplify được tách biệt khỏi infrastructure backend.
- Deployment có thể được quản lý thông qua Git-based workflow.

Kiến trúc frontend/backend sau deployment:

Frontend

&nbsp;&nbsp;↓

Amplify

&nbsp;&nbsp;↓

CloudFront

&nbsp;&nbsp;↓

ALB

&nbsp;&nbsp;↓

EC2

&nbsp;&nbsp;↓

RDS

![ALB as CloudFront Origin](images/4-Workshop/4.7-Amplify/1.png)