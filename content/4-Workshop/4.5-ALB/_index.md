---
title: "Application Load Balancer"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.5. </b> "
---

# Application Load Balancer

Application Load Balancer (ALB) is used in the KnoVerse architecture to receive HTTP requests to the backend and route requests to the EC2 instance running the backend application.

In the current architecture, ALB acts as the intermediate access point between CloudFront and the EC2 backend, while also providing backend health checking through Target Group and Health Check.

#### Content

1. [ALB Overview](4.5.1-ALB-overview/)

2. [ALB Deployment](4.5.2-ALB-deployment/)

3. [ALB Verification](4.5.3-ALB-verification/)
