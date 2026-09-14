---

title: "Cập nhật hệ thống và cài đặt Node.js"

date: 2026-09-14

weight: 5

chapter: false

pre: " <b> 4.4.2.5. </b> "

---

Sau khi đăng nhập vào EC2 instance, cập nhật các system packages:

sudo dnf update -y

Kiểm tra hệ điều hành:

cat /etc/os-release

Sau đó cài đặt Node.js theo version phù hợp với backend.

Kiểm tra version đã cài đặt:

node -v

npm -v

Kết quả cần xác nhận Node.js và npm đã được cài đặt thành công.

![Cài đặt Node.js](/images/4-Workshop/4.4-EC2/7.png)

