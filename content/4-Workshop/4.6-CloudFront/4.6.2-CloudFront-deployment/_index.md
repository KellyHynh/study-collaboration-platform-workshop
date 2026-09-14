---

title: "Amazon CloudFront Deployment"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.6.2. </b> "

---

# Amazon CloudFront Deployment

This section describes the complete CloudFront deployment process in the order it is performed in practice. CloudFront uses the Application Load Balancer as its origin, so the deployment verifies the CloudFront -> ALB -> EC2 -> RDS connection.

#### 4.6.2.1. Prepare the Origin

Before creating the CloudFront distribution, make sure the ALB is operating normally.

Test the ALB directly:

curl.exe -v http://<ALB-DNS>/api/courses

Expected result:

HTTP/1.1 200 OK

The response should contain course data. If the ALB does not return 200 OK, do not continue troubleshooting CloudFront.

#### 4.6.2.2. Create a CloudFront Distribution

Open:

AWS Console -> CloudFront -> Distributions -> Create distribution

Set an appropriate distribution name, for example:

knoverse-backend-api

#### 4.6.2.3. Configure the Origin

In the Origin section, enter the DNS name of the ALB.

Example:

knoverse-backend-alb-xxxxxxxx.ap-southeast-1.elb.amazonaws.com
![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/2.png)

Do not use the EC2 public IP as the CloudFront origin. The ALB is the intermediary origin for managing traffic to the backend.

#### 4.6.2.4. Configure the Origin Protocol

The current KnoVerse origin uses:

HTTP
![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/3.png)

CloudFront uses HTTP to connect to the ALB while HTTPS between the client and CloudFront is maintained.

#### 4.6.2.5. Configure the Viewer Protocol Policy

In Behavior, set:

Viewer protocol policy:
Redirect HTTP to HTTPS

The official API endpoint is:

https://d2hvns14tchtf3.cloudfront.net/api/courses

#### 4.6.2.6. Configure Allowed HTTP Methods

The current configuration allows:

GET
HEAD
POST
PUT
PATCH
DELETE
OPTIONS

These methods allow CloudFront to forward the backend CRUD requests to the ALB.

#### 4.6.2.7. Configure the Cache Policy

The KnoVerse backend API uses:

Managed-CachingDisabled

This forwards requests to the backend instead of returning stale data from the CloudFront cache. Caching is not appropriate for the current CRUD mutation APIs.

The current architecture prioritizes:

Client
  ↓
CloudFront
  ↓
ALB
  ↓
Backend

#### 4.6.2.8. Configure CloudFront Behavior

Default behavior:

Path pattern:
Default (*)
Origin:
knoverse-backend-alb
Viewer protocol:
Redirect HTTP to HTTPS
Allowed methods:
GET, HEAD, POST, OPTIONS, PUT, PATCH, DELETE
Cache policy:
Managed-CachingDisabled

The current implementation does not use CloudFront Functions or Lambda@Edge.

#### 4.6.2.9. Configure HTTPS

After deployment, CloudFront provides:

https://d2hvns14tchtf3.cloudfront.net

Clients can use this endpoint instead of the EC2 public address.

#### 4.6.2.10. Deploy the Distribution

Create the distribution after completing the configuration. Wait for deployment to complete before evaluating the endpoint because the configuration may not be applied immediately at all edge locations.

#### 4.6.2.11. Test the CloudFront Endpoint

After deployment, test:

curl.exe -v https://d2hvns14tchtf3.cloudfront.net/api/courses

Expected result:

HTTP/1.1 200 OK

The response body contains course data. The end-to-end flow is:

CloudFront
    ↓
ALB
    ↓
EC2
    ↓
Backend
    ↓
RDS

#### 4.6.2.12. Test from an External Network

Test the CloudFront URL from another computer, phone, network, or mobile data:

https://d2hvns14tchtf3.cloudfront.net/api/courses

A successful response from another network demonstrates that the application is exposed through AWS infrastructure rather than only running locally.

#### 4.6.2.13. Integration with the Frontend

The KnoVerse frontend is deployed separately on AWS Amplify and uses the CloudFront endpoint as its backend API endpoint.
![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/image.png)

The frontend can call:

GET https://d2hvns14tchtf3.cloudfront.net/api/courses

instead of:

GET http://localhost:3000/api/courses

