---

title: "Kết nối tới EC2 bằng SSH"

date: 2026-09-14

weight: 4

chapter: false

pre: " <b> 4.4.2.4. </b> "

---

Sau khi instance được tạo, sử dụng SSH để truy cập server.

Ví dụ:

ssh -i <key-file> ec2-user@<EC2_PUBLIC_IP>

Sau khi kết nối thành công, terminal sẽ chuyển sang môi trường của EC2 instance.

Ví dụ:

[ec2-user@ip-172-31-xx-xxx ~]$

Từ thời điểm này, các lệnh tiếp theo được thực hiện trực tiếp trên EC2 instance.

![Kết nối tới EC2 bằng SSH](images/4-Workshop/4.4-EC2/6.png)

