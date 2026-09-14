---

title: "Kiểm tra Backend API trên EC2"

date: 2026-09-14

weight: 10

chapter: false

pre: " <b> 4.4.2.10. </b> "

---

Trước khi tích hợp ALB, cần xác nhận backend application thực sự hoạt động.

Từ EC2 hoặc một môi trường có thể truy cập backend, thực hiện:

curl http://localhost:3000/api/courses

Nếu backend hoạt động đúng, API sẽ trả về course data.

Có thể kiểm tra HTTP status:

curl -i http://localhost:3000/api/courses

Kết quả mong đợi:

HTTP/1.1 200 OK

![Kiểm tra Backend API](images/4-Workshop/4.4-EC2/9.png)

