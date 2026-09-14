---

title: "Triển khai Amazon Amplify"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.7.2. </b> "

---

# Triển khai Amazon Amplify

Phần này trình bày toàn bộ quy trình triển khai frontend KnoVerse lên Amazon Amplify.

#### 4.7.2.1. Chuẩn bị frontend application

Trước khi triển khai, frontend KnoVerse cần:

- Có source code hoàn chỉnh.
- Có repository chứa source code.
- Project có thể build thành công ở local.
- Các API endpoint cần được xác định rõ.

Đối với môi trường local, frontend có thể sử dụng Vite development server và proxy:

server: {
    proxy: {
        "/api": {
            target: "http://localhost:3000",
            changeOrigin: true,
        },
    },
},

Khi triển khai production, frontend cần sử dụng backend endpoint được triển khai trên AWS thay vì phụ thuộc vào localhost.

#### 4.7.2.2. Tạo Amplify application

Truy cập AWS Management Console -> Amplify.

Chọn tùy chọn tạo hoặc host web application và kết nối với repository chứa source code của KnoVerse.

Chọn:

1. Git provider.
2. Repository của project.
3. Branch cần triển khai.

Branch production là:

main

#### 4.7.2.3. Cấu hình build settings

Amplify cần biết cách cài đặt dependencies và build frontend.

Đối với ứng dụng sử dụng Vite, quá trình build gồm:

Install dependencies
        ↓
Run build command
        ↓
Generate production files
        ↓
Deploy generated files

Build command của project cần tương ứng với cấu hình trong `package.json`.

Ví dụ:

npm run build

Sau khi build thành công, các file frontend production được Amplify triển khai.

#### 4.7.2.4. Cấu hình Environment Variables

Các giá trị cấu hình khác nhau giữa môi trường development và production có thể được khai báo thông qua Amplify Environment Variables.

Ví dụ:

API_BASE_URL

Production application có thể sử dụng endpoint AWS thay vì:

http://localhost:3000

Environment variables giúp tách configuration khỏi source code và thuận tiện hơn khi chuyển đổi giữa các môi trường.

Trong quá trình triển khai KnoVerse, environment variables được kiểm tra tại:

Amplify -> App -> Environment variables

Không đưa secret hoặc credential nhạy cảm trực tiếp vào frontend environment variables vì giá trị được sử dụng trong frontend có thể trở thành một phần của client-side application.

#### 4.7.2.5. Deploy branch main

Sau khi hoàn tất cấu hình, bắt đầu deployment.

Amplify thực hiện các bước:

Source Code
    ↓
Clone Repository
    ↓
Install Dependencies
    ↓
Build
    ↓
Deploy
    ↓
Production Hosting

Theo dõi trạng thái deployment trong Amplify. Trạng thái thành công cho biết deployment đã hoàn tất.

#### 4.7.2.6. Kiểm tra production URL

Sau khi deployment hoàn tất, Amplify cung cấp production URL.

Địa chỉ production application hiện tại của KnoVerse là:

https://main.d2hfdjfyze730o.amplifyapp.com/

Kết quả mong đợi:

- Website hiển thị bình thường.
- Các trang frontend có thể truy cập.
- Không xuất hiện lỗi build hoặc deployment.
- Frontend có thể thực hiện API request đến backend AWS.

#### 4.7.2.7. Kiểm tra kết nối Frontend – Backend

Deployment frontend
chỉ được xem là hoàn chỉnh khi frontend có thể giao tiếp với backend
production.

Kiến trúc request:
![ALB as CloudFront Origin](/images/4-Workshop/4.7-Amplify/image.png)

Frontend thực hiện
request tới API:

`/api/courses`

Backend xử lý
request và truy xuất course data từ RDS.

Sau đó dữ liệu được
trả về frontend để hiển thị.

Kết quả thực tế của
KnoVerse cho thấy production website có thể tải **course
data** thành công.

Đây là evidence quan
trọng vì nó chứng minh **frontend production đã giao tiếp thành công với
backend AWS**, thay vì chỉ chứng minh rằng website trên Amplify có thể được
mở.

#### 4.7.2.8. Kiểm tra từ môi trường mạng khác

Để xác minh
application không phụ thuộc vào môi trường local, production URL có thể được
truy cập từ một thiết bị hoặc mạng khác.

Ví dụ:

Device A

```
│

└── Production Internet

         ↓

      Amplify

         ↓

      AWS Backend
```

Nếu website vẫn có
thể truy cập và hiển thị course data, deployment đã đạt được mục tiêu public
accessibility.
