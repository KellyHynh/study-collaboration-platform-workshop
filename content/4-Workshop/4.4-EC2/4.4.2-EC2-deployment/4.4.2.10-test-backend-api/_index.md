---

title: "Test Backend API on EC2"

date: 2026-09-14

weight: 10

chapter: false

pre: " <b> 4.4.2.10. </b> "

---

Before integrating the ALB, verify that the backend application is actually working.

From the EC2 instance or an environment that can access the backend, run:

curl http://localhost:3000/api/courses

If the backend is working correctly, the API returns course data.

The HTTP status can also be checked:

curl -i http://localhost:3000/api/courses

Expected result:

HTTP/1.1 200 OK

![Backend API Test](images/4-Workshop/4.4-EC2/9.png)
