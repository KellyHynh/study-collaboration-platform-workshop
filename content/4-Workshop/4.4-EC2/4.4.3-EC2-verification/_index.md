---

title: "EC2 Verification"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.4.3. </b> "

---

#### 4.4.3.1. Backend Application Testing

The basic tests include:

| **Test**         | **Expected Result** |
| ---------------- | ------------------- |
| EC2 instance     | Running             |
| Node.js          | Installed           |
| Backend process  | Running             |
| Local API        | 200 OK              |
| RDS connection   | Successful          |
| Database query   | Successful          |
| ALB target       | Healthy             |
| ALB /api/courses | 200 OK              |

These tests verify each layer before moving to the next layer.

#### 4.4.3.2. End-to-End Testing

After integrating EC2 with the ALB, test the complete backend flow:

HTTP Request

    │

    ▼

    ALB

    │

    ▼

Target Group

    │

    ▼

    EC2

    │

    ▼

KnoVerse Backend

    │

    ▼

    RDS

    │

    ▼

Course Data

Test endpoint:

GET /api/courses

The expected result is HTTP 200 OK together with course data.

#### 4.4.3.3. Common Issues and Troubleshooting

**EC2 SSH connection fails**

Check:

- Key pair.

- Public IP.

- Security Group port 22.

- Network configuration.

**Backend does not start**

Check:

- Node.js version.

- Dependencies.

- package.json.

- Environment variables.

- Application logs.

**Backend cannot connect to RDS**

Check:

- RDS status.

- RDS endpoint.

- Port 5432.

- RDS Security Group.

- EC2 Security Group.

- Database credentials.

**ALB target is Unhealthy**

Check:

1. Whether the backend is running.

2. Whether the backend is listening on the correct port.

3. Whether the Target Group is using the correct port.

4. Whether the health check path is correct.

5. Whether the EC2 Security Group allows traffic from the ALB Security Group.

#### 4.4.3.4. Evaluation and Optimization

After the backend is running, the EC2 configuration can be evaluated based on:

- CPU utilization.

- Memory usage.

- Network traffic.

- Application response time.

- Instance capacity.

- Application availability.

As the workload increases, the following options can be considered:

- Changing the instance type.

- Using Auto Scaling.

- Running multiple EC2 instances behind the ALB.

- Using a process manager to maintain the backend process.

- Monitoring application and infrastructure metrics using Amazon CloudWatch.

For the current demo environment, a single EC2 instance behind the ALB is sufficient to demonstrate the architecture and deployment flow.

#### 4.4.3.5. Results

After completing the deployment:

- The KnoVerse backend runs on Amazon EC2.

- EC2 is deployed within the AWS VPC.

- The Security Group controls traffic to the application.

- The backend successfully connects to Amazon RDS.

- The Application Load Balancer distributes requests to EC2.

- EC2 is confirmed as Healthy by the Target Group.

- The /api/courses API works through the ALB.

- The backend becomes the application layer of the KnoVerse architecture on AWS.

The architecture after completing the EC2 deployment is shown below:

![EC2 Deployment Architecture](images/4-Workshop/4.4-EC2/1.png)

