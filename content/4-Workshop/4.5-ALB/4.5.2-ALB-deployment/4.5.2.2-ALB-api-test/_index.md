---
title: "Test ALB Endpoint and CloudFront Integration"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 4.5.2.2. </b> "
---

#### 4.5.2.8. Configure Security Group for ALB

Create or use a Security Group dedicated to ALB.

Example:

Security Group:

knoverse-alb-sg

Inbound rule:

Type: HTTP

Protocol: TCP

Port: 80

Source: 0.0.0.0/0

This rule allows HTTP traffic to the ALB.

Outbound traffic can be allowed according to the default configuration:

All traffic → 0.0.0.0/0

#### 4.5.2.9. Configure Listener

Listener defines the protocol and port used by ALB to receive requests.

Create a listener:

Protocol: HTTP

Port: 80

Default action:

Forward to:

knoverse-backend-tg

When a request arrives at:

[http://<ALB-DNS>/api/courses]

ALB forwards the request to the Target Group.

The Target Group then forwards the request to:

EC2:3000


#### 4.5.2.10. Check Target Health

After ALB and the Target Group are configured, return to:

**Target Groups → knoverse-backend-tg → Targets**

Check the status of EC2.

Expected result:

Status: Healthy

If the target is Unhealthy, check:

1. Is the backend running?
2. Is the backend listening on port 3000?
3. Is the Health Check path correct?
4. Does the EC2 Security Group allow traffic from the ALB Security Group?
5. Is the network configuration correct?
