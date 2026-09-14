---
title: "ALB Verification"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.5.3. </b> "
---

**#### 4.5.3.1. Layer-by-Layer Testing**

To identify the exact layer where an issue occurs, test in the following order:

**Layer 1 — Backend**

EC2 →

localhost:3000/api/courses

Expected:

200 OK

**Layer 2 — ALB**

ALB-DNS/api/courses

Expected:

200 OK

**Layer 3 — CloudFront**

CloudFront-Domain/api/courses

Expected:

200 OK

Testing each layer separately helps avoid changing multiple AWS services at the same time during troubleshooting.

**#### 4.5.3.2. Health Check Status**

Target Group provides the following statuses:

Healthy

Unhealthy

Initial

Draining

In the completed deployment, the EC2 target should maintain the status:

Healthy

If the status changes unexpectedly, check the application and network configuration.

**#### 4.5.3.3. Performance Metrics**

ALB metrics can be used to monitor:

- Request count.
- HTTP response codes.
- Target response time.
- Healthy target count.
- Unhealthy target count.

These metrics help evaluate how ALB processes requests and whether the backend responds consistently.

**#### 4.5.3.4. Common Issues**

**ALB returns 502 Bad Gateway**

Possible causes include:

- EC2 backend is not running.
- Backend is not listening on port 3000.
- Target Group uses the wrong port.
- Security Group blocks traffic.
- Application closes the connection or does not return a valid response.

**ALB returns 503 Service Unavailable**

Check whether the Target Group has a Healthy target.

**CloudFront returns 502/504**

Check in the following order:

CloudFront
  ↓
ALB
  ↓
Target Group
  ↓
EC2
  ↓
Backend

First confirm:

ALB /api/courses → 200 OK

If ALB already returns 200 OK but CloudFront still fails, focus on the CloudFront Origin and behavior configuration instead of continuing to change EC2.

**#### 4.5.3.5. Architecture Optimization**

For the current workload, one EC2 instance is sufficient for demonstration.

However, the ALB architecture can scale:

ALB
     /       \
    ▼         ▼
  EC2-1     EC2-2
     \       /
      ▼     ▼
         RDS

When workload increases, the architecture can:

- Add multiple EC2 instances.
- Register multiple targets in the Target Group.
- Use an Auto Scaling Group.
- Distribute traffic across multiple instances.
- Use health checks to remove unhealthy targets.

This allows the architecture to scale without changing the endpoint used by clients.

**#### 4.5.3.6. Achieved Results**

After completing the ALB deployment:

- Application Load Balancer was successfully created for KnoVerse.
- ALB was deployed as Internet-facing.
- ALB uses multiple Availability Zones.
- Target Group was configured for the EC2 backend.
- Health Check confirmed the EC2 backend as Healthy.
- HTTP port 80 Listener forwards requests to the backend Target Group.
- ALB can access /api/courses and receive course data.
- ALB is used as the origin for CloudFront.
- The backend flow from CloudFront → ALB → EC2 → RDS is completed.
