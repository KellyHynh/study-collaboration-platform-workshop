---

title: "Chuẩn bị Backend Application"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.4.2.1. </b> "

---

Trước khi tạo EC2 instance, cần đảm bảo backend application của KnoVerse có thể chạy bình thường trong môi trường local.

#### Kiểm tra Backend Dependencies

Cài đặt các dependencies cần thiết:

npm install

Sau khi cài đặt dependencies, khởi động backend application:

npm start

hoặc sử dụng command tương ứng được định nghĩa trong `package.json`.

#### Kiểm tra Backend API

Kiểm tra API endpoint sau:

GET /api/courses

Backend cần trả về course data thành công trước khi bắt đầu quá trình triển khai lên AWS.

![Kiểm tra Backend API](/images/4-Workshop/4.4-EC2/2.png)

Điều này giúp phân biệt các vấn đề liên quan đến application với các lỗi có thể phát sinh trong quá trình triển khai AWS.

