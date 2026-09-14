---

title: "Kiểm tra API thông qua ALB"

date: 2026-09-14

weight: 12

chapter: false

pre: " <b> 4.4.2.12. </b> "

---

Sau khi target trở thành **Healthy**, sử dụng ALB DNS name để kiểm tra backend.

Ví dụ:

curl -v http://<ALB-DNS-NAME>/api/courses

Kết quả mong đợi:

HTTP/1.1 200 OK

và response chứa course data.

Đây là bước xác nhận flow sau đã hoạt động end-to-end:

ALB

↓

Target Group

↓

EC2

↓

Backend

↓

RDS

![Kiểm tra API thông qua ALB](/images/4-Workshop/4.4-EC2/11.png)

