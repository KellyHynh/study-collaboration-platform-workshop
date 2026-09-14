---

title: "Integrate EC2 with Application Load Balancer"

date: 2026-09-14

weight: 11

chapter: false

pre: " <b> 4.4.2.11. </b> "

---

After the backend is running stably on EC2, the instance is added to the Target Group of the Application Load Balancer.

The traffic flow is:

Client

 │

 ▼

Application Load Balancer

 │

 ▼

Target Group

 │

 ▼

EC2 :3000

The Target Group needs to be configured with:

Protocol: HTTP

Port: 3000

The health check uses an appropriate endpoint to determine whether the backend is operating correctly.

After the EC2 instance is registered with the Target Group, check the target health.

Expected status:

Healthy

![EC2 Target Group](images/4-Workshop/4.4-EC2/10.png)

