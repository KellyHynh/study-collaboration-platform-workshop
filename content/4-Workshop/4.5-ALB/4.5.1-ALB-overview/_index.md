---
title: "Application Load Balancer Overview"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.5.1. </b> "
---

#### 4.5.1.1. Role in the KnoVerse Architecture

ALB is positioned between CloudFront and EC2.

![KnoVerse ALB Architecture](images/4-Workshop/4.5-ALB/1.png)

When a client sends a request to the API, the request is sent to ALB. ALB then forwards the request to the appropriate target in the Target Group.

For the endpoint:

GET /api/courses

the request flow is:

GET /api/courses
        │
        ▼
CloudFront
        │
        ▼
ALB :80
        │
        ▼
Target Group
        │
        ▼
EC2 :3000
        │
        ▼
Express Backend
        │
        ▼
RDS PostgreSQL

#### 4.5.1.2. Purpose of Using ALB

ALB is used to:

- Provide a stable endpoint for the backend.
- Avoid requiring clients to access EC2 directly.
- Route HTTP requests to the backend.
- Check the status of EC2 through health checks.
- Act as an origin for CloudFront.
- Allow the architecture to scale to additional EC2 instances in the future.

Using ALB also separates the public access layer from the application server layer.

#### 4.5.1.3. Why Choose ALB?

ALB is suitable for KnoVerse because the backend uses HTTP/REST APIs and requires a Layer 7 routing component.

ALB supports:

- HTTP/HTTPS.
- Path-based routing.
- Target Groups.
- Health Checks.
- Integration with EC2.
- Integration with CloudFront.
- Scaling to multiple backend instances.

For the current project, ALB is mainly used to route requests to EC2 and act as the origin for CloudFront.
