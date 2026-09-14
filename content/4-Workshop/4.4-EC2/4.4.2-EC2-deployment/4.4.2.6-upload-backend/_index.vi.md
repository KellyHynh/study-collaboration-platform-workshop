---

title: "Đưa Backend Source Code lên EC2"

date: 2026-09-14

weight: 6

chapter: false

pre: " <b> 4.4.2.6. </b> "

---

Source code của backend cần được đưa lên EC2 instance.

Có thể sử dụng Git để clone repository:

git clone <repository-url>

Sau đó chuyển vào backend directory:

cd <backend-directory>

Kiểm tra source code:

ls

Sau đó cài đặt các dependencies cần thiết:

npm install

Kiểm tra `package.json` và đảm bảo các dependencies cần thiết của backend đã được cài đặt.

