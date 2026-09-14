---

title: "Cấu hình Security Group cho EC2"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.4.2.3. </b> "

---

Security Group kiểm soát traffic đến EC2 backend.

Backend KnoVerse sử dụng port:

3000

Do đó cần xác định các traffic cần thiết cho application.

#### SSH

SSH được sử dụng để quản trị EC2:

Type:

SSH

Protocol: TCP

Port: 22

Source: Administrator's IP

Không nên mở SSH cho toàn bộ Internet nếu không cần thiết.

#### Backend Traffic

Backend cần nhận traffic từ Application Load Balancer.

Về nguyên tắc:

ALB

 │

 │ HTTP :3000

 ▼

EC2

Security Group của EC2 nên cho phép port backend từ Security Group của ALB thay vì mở port 3000 cho toàn bộ Internet.

![EC2 Security Group](/images/4-Workshop/4.4-EC2/5.png)

