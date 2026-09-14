---

title: "Triển khai EC2"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.4.2. </b> "

---

Phần này trình bày toàn bộ quy trình triển khai backend application của KnoVerse trên Amazon EC2. Quá trình triển khai được thực hiện theo trình tự thực tế, từ chuẩn bị backend application và tạo EC2 instance đến cấu hình environment, kết nối với Amazon RDS, khởi động backend và tích hợp với Application Load Balancer.

#### Nội dung

1. [Chuẩn bị Backend Application](4.4.2.1-prepare-backend/)

2. [Tạo EC2 Instance](4.4.2.2-create-ec2/)

3. [Cấu hình Security Group cho EC2](4.4.2.3-ec2-security-group/)

4. [Kết nối tới EC2 bằng SSH](4.4.2.4-ec2-ssh/)

5. [Cập nhật hệ thống và cài đặt Node.js](4.4.2.5-install-nodejs/)

6. [Đưa Backend Source Code lên EC2](4.4.2.6-upload-backend/)

7. [Cấu hình Environment Variables](4.4.2.7-environment-variables/)

8. [Kết nối EC2 với Amazon RDS](4.4.2.8-ec2-rds-connection/)

9. [Khởi động Backend Application](4.4.2.9-start-backend/)

10. [Kiểm tra Backend API trên EC2](4.4.2.10-test-backend-api/)

11. [Tích hợp EC2 với Application Load Balancer](4.4.2.11-ec2-alb/)

12. [Kiểm tra API thông qua ALB](4.4.2.12-test-api-alb/)

