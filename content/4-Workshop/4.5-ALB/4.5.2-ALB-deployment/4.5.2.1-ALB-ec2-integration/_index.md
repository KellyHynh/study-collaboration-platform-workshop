---
title: "Prepare and Configure ALB"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.5.2.1. </b> "
---

#### 4.5.2.1. Prepare Before Creating ALB

Before creating ALB, ensure:

- EC2 instance has been created.
- Backend application is running.
- Backend is listening on the correct port.
- VPC has been configured.
- At least two Availability Zones/subnets are available for ALB.
- Security Groups have been prepared.

In KnoVerse, the backend currently runs on:

EC2 → port 3000

ALB will receive HTTP requests on:

ALB → port 80

and forward them to:

EC2 → port 3000

#### 4.5.2.2. Create Target Group

Target Group identifies the backend target to which ALB forwards requests.

Go to:

**EC2 → Target Groups → Create target group**

Select:

Target type: Instances

Protocol: HTTP

Port: 3000

Example name:

knoverse-backend-tg

Select the VPC used by KnoVerse.

#### 4.5.2.3. Configure Health Check

Health Check is used to determine whether the target is operating.

Configuration:

Protocol: HTTP

Port: Traffic port

Path: /api/courses

If /api/courses returns a successful response, the target can be identified as healthy.

A separate health endpoint may be used in the future, for example:

GET /health

For the current implementation, /api/courses can be used to confirm that the backend is responding.


#### 4.5.2.4. Register EC2 Instance in Target Group

At **Register targets**, select the KnoVerse EC2 instance.

Select port:

3000

Then select:

**Include as pending below → Register pending targets**

The target will appear in the Target Group.

The initial status may be:

Initial

After ALB performs the health check, the status will become:

Healthy

if the backend responds correctly.


#### 4.5.2.5. Create Application Load Balancer

Go to:

**EC2 → Load Balancers → Create Load Balancer**

Select:

Application Load Balancer

Set the name:

knoverse-backend-alb

#### 4.5.2.6. Configure Scheme

Select:

Scheme: Internet-facing

This allows ALB to receive traffic from outside the VPC.

This configuration is suitable for the current architecture because CloudFront needs to access the ALB origin.

IP address type:

IPv4

#### 4.5.2.7. Select VPC and Availability Zones

Select the KnoVerse VPC:

vpc-0a94136df6e8c9a03

Select at least two Availability Zones.

Example:

ap-southeast-1c

ap-southeast-1a

with the corresponding subnets.

Using multiple Availability Zones helps ALB operate more reliably if an Availability Zone experiences a failure.
