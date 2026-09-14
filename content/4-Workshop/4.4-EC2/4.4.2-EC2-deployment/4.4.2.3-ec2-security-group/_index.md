---

title: "Configure Security Group for EC2"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.4.2.3. </b> "

---

Security Group controls traffic to the EC2 backend.

The KnoVerse backend uses the following port:

3000

Therefore, the required traffic for the application needs to be configured.

#### SSH

SSH is used to administer the EC2 instance:

Type:

SSH

Protocol: TCP

Port: 22

Source: Administrator's IP

SSH should not be opened to the entire Internet unless necessary.

#### Backend Traffic

The backend needs to receive traffic from the Application Load Balancer.

The traffic flow is:

ALB

 │

 │ HTTP :3000

 ▼

EC2

The EC2 Security Group should allow the backend port from the ALB Security Group instead of opening port 3000 to the entire Internet.

![EC2 Security Group](/images/4-Workshop/4.4-EC2/5.png)

