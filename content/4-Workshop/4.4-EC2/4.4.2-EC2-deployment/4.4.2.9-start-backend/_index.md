---

title: "Start Backend Application"

date: 2026-09-14

weight: 9

chapter: false

pre: " <b> 4.4.2.9. </b> "

---

From the backend directory:

npm start

The backend will start listening on the port specified by the application configuration, for example:

3000

The process/application can be checked through the terminal.

![Backend Application Running](/images/4-Workshop/4.4-EC2/8.png)

At this point, the backend is running on EC2 but does not necessarily need to be directly exposed to end users.

The architecture at this stage is:

Internet

  │

  ▼

EC2 Backend

  │

  ▼

RDS

After the ALB is integrated, traffic will go through the Load Balancer instead of accessing the EC2 instance directly.

