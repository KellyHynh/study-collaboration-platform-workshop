---
title: "ALB API Test and CloudFront Integration"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.5.2.3. </b> "
---

#### 4.5.2.11. Test ALB Endpoint

After the target becomes Healthy, obtain the **DNS name** of the ALB.

Example:

knoverse-backend-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com

Test:

curl.exe -v http://<ALB-DNS>/api/courses

Expected result:

HTTP/1.1 200 OK

Content-Type: application/json

The response must contain course data from KnoVerse.

This confirms that ALB successfully forwards the request to the EC2 backend.


#### 4.5.2.12. Integrate ALB with CloudFront

After ALB operates correctly, ALB is used as the **origin** for the CloudFront distribution knoverse-backend-api.

![ALB as CloudFront Origin](images/4-Workshop/4.5-ALB/image.png)

In CloudFront, configure the origin to point to the ALB DNS:

knoverse-backend-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com

CloudFront then receives requests from the frontend and forwards requests to ALB.

#### 4.5.2.13. Test API Through CloudFront

After the CloudFront distribution completes deployment, test:

curl.exe -v https://<CLOUDFRONT-DOMAIN>/api/courses

Example:

curl.exe -v https://d2hvns14tchtf3.cloudfront.net/api/courses

Expected result:

HTTP/1.1 200 OK

and the response contains course data.

When this step succeeds, the request has passed through the backend architecture:

CloudFront
    ↓
ALB
    ↓
Target Group
    ↓
EC2
    ↓
Backend
    ↓
RDS


If CloudFront returns 502 or 504 during configuration, do not immediately conclude that EC2 or ALB is faulty. Check each layer separately by calling the ALB directly first, then check the CloudFront origin connection.
