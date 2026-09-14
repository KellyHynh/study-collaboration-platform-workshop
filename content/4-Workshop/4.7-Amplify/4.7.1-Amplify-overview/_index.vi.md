---

title: "Tổng quan về Amazon Amplify"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.7.1. </b> "

---

# Tổng quan về Amazon Amplify

#### 4.7.1.1. Vai trò trong kiến trúc KnoVerse

Amazon Amplify được sử dụng để triển khai và hosting frontend của hệ thống KnoVerse.

Frontend của KnoVerse được phát triển dưới dạng web application và được lưu trữ trong repository. Amplify kết nối với repository này để thực hiện quá trình build và deployment, sau đó cung cấp một URL public để người dùng truy cập ứng dụng.

Trong kiến trúc tổng thể, Amplify đảm nhiệm lớp frontend:

Amplify

&nbsp;&nbsp;↓

Frontend

![ALB as CloudFront Origin](/images/4-Workshop/4.7-Amplify/1.png)

Amplify tập trung vào frontend hosting và deployment, trong khi backend và database được triển khai trên các dịch vụ AWS khác.

#### 4.7.1.2. Lý do lựa chọn Amazon Amplify

Amazon Amplify được lựa chọn cho frontend của KnoVerse vì cung cấp quy trình triển khai web application tương đối đơn giản và phù hợp với mô hình phát triển sử dụng Git repository.

Các lợi ích chính:

- Tích hợp trực tiếp với source code repository.
- Tự động build và deploy khi source code được cập nhật.
- Cung cấp production URL cho frontend.
- Hỗ trợ quản lý environment variables.
- Giảm nhu cầu tự cấu hình web server cho frontend.
- Phù hợp với quá trình phát triển và demo project.

Trong phạm vi KnoVerse, Amplify giúp tách frontend khỏi EC2 backend, nhờ đó mỗi thành phần có thể được triển khai và quản lý độc lập.

