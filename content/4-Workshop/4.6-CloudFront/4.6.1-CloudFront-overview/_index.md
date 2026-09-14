---

title: "Amazon CloudFront Overview"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.6.1. </b> "

---

# Amazon CloudFront Overview

#### 4.6.1.1. Role in the KnoVerse Architecture

CloudFront is located at the outermost layer of the backend architecture.

![ALB as CloudFront Origin](/images/4-Workshop/4.6-CloudFront/1.png)

CloudFront provides a public endpoint for the backend:

https://<cloudfront-domain>

Example in KnoVerse:

https://d2hvns14tchtf3.cloudfront.net

The API can be accessed through:

https://d2hvns14tchtf3.cloudfront.net/api/courses

#### 4.6.1.2. Purpose of Use

CloudFront is used to:

- Provide a public endpoint for the application.
- Stand before the ALB in the backend architecture.
- Support HTTPS for client connections.
- Distribute requests through the AWS edge network.
- Provide an intermediary layer between the client and origin.
- Allow security and caching policies to be applied.
- Support integration with AWS WAF for request control.

In KnoVerse, CloudFront does not access EC2 directly. Requests are forwarded to the ALB, and the ALB then forwards the requests to the backend.

#### 4.6.1.3. Why Choose CloudFront

CloudFront fits the KnoVerse architecture because the system needs a public endpoint that can be accessed from different networks.

CloudFront also allows the architecture to be extended in the future to serve:

- Static assets.
- API.
- Frontend content.
- Cached resources.
- HTTPS traffic.
- WAF protection.

For the workshop, using CloudFront demonstrates how an AWS CDN/distribution can be integrated with a backend application running on EC2 through an ALB.
