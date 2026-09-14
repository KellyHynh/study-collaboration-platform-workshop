---

title: "Test API Through ALB"

date: 2026-09-14

weight: 12

chapter: false

pre: " <b> 4.4.2.12. </b> "

---

After the target becomes **Healthy**, use the ALB DNS name to test the backend.

For example:

curl -v http://<ALB-DNS-NAME>/api/courses

Expected result:

HTTP/1.1 200 OK

and the response contains course data.

This confirms that the following flow is working end-to-end:

ALB

↓

Target Group

↓

EC2

↓

Backend

↓

RDS

![Test API Through ALB](images/4-Workshop/4.4-EC2/11.png)

