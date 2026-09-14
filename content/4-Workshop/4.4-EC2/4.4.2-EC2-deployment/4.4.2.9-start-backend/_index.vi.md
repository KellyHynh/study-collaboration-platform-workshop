---

title: "Khởi động Backend Application"

date: 2026-09-14

weight: 9

chapter: false

pre: " <b> 4.4.2.9. </b> "

---

Từ backend directory:

npm start

Backend sẽ bắt đầu lắng nghe trên port được application configuration chỉ định, ví dụ:

3000

Có thể kiểm tra process/application bằng terminal.

![Backend Application Running](images/4-Workshop/4.4-EC2/8.png)

Backend lúc này hoạt động trên EC2 nhưng chưa nhất thiết phải được expose trực tiếp cho người dùng cuối.

Kiến trúc tại thời điểm này:

Internet

  │

  ▼

EC2 Backend

  │

  ▼

RDS

Sau khi ALB được tích hợp, traffic sẽ đi qua Load Balancer thay vì truy cập trực tiếp EC2.

