---

title: "CloudFront Verification"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.6.3. </b> "

---

# CloudFront Verification

#### 4.6.3.1. Layer-by-Layer Testing

To troubleshoot CloudFront, check the layers in this order:

Step 1 - EC2

EC2 -> Backend -> RDS

Check whether the backend returns data.

Step 2 - ALB

ALB /api/courses

Expected:

200 OK

Step 3 - CloudFront

CloudFront /api/courses

Expected:

200 OK

This approach helps identify the exact layer causing the problem.

#### 4.6.3.2. Check CloudFront Metrics

The following metrics can be monitored:

- Requests.
- Bytes downloaded.
- Error rate.
- HTTP status.
- Cache behavior.

These metrics help determine whether the distribution is receiving requests and whether requests are being processed successfully.

#### 4.6.3.3. Analyze HTTP Status Codes

| **Status** | **Meaning in troubleshooting** |
| --- | --- |
| 200 | Request successful |
| 301/302 | Redirect, usually HTTP to HTTPS |
| 403 | Request rejected |
| 502 | CloudFront did not receive a valid response from the origin |
| 504 | CloudFront did not receive a response from the origin within the allowed time |

When CloudFront returns 502 or 504, check the ALB origin first. If the ALB also fails, the problem is in the ALB, EC2, or backend. If the ALB returns 200 but CloudFront fails, focus on the CloudFront origin configuration and origin connection.

#### 4.6.3.4. Potential Issues

**CloudFront Returns 502 Bad Gateway**

Check:

- Origin DNS.
- Origin protocol.
- Origin port.
- ALB listener.
- Target Group.
- EC2 backend.

**CloudFront Returns 504 Gateway Timeout**

Check:

- Whether the ALB responds.
- Whether EC2 is running.
- Whether the backend has timed out.
- Whether the target is healthy.
- Network and Security Group configuration.

**CloudFront Returns 403**

Check:

- WAF rules.
- CloudFront behavior.
- Allowed methods.
- Origin configuration.
- Request restrictions.

#### 4.6.3.5. Caching Optimization

The current API uses Managed-CachingDisabled because data changes frequently during the CRUD backend stage.

In the future, infrequently changing resources such as `/static/*` and `/assets/*` can be cached while mutation APIs continue to bypass the cache.

#### 4.6.3.6. AWS WAF Integration

CloudFront can integrate with AWS WAF to protect the application from unwanted requests. In KnoVerse, WAF has been enabled on the CloudFront distribution.

WAF can be used to:

- Control requests.
- Block malicious traffic.
- Rate limit traffic.
- Monitor request patterns.
- Add a security layer before the origin.

The flow is:

Client
  ↓
CloudFront
  ↓
AWS WAF
  ↓
ALB
  ↓
EC2

WAF operates at the edge/security layer and does not replace Security Groups or other network security mechanisms.

#### 4.6.3.7. Achieved Results

After completing the CloudFront deployment:

- The CloudFront distribution `knoverse-backend-api` is created.
- The ALB is configured as the CloudFront origin.
- Clients use HTTPS to access the backend.
- HTTP requests redirect to HTTPS.
- CloudFront supports the HTTP methods required by the backend CRUD API.
- API caching is disabled so requests are forwarded to the backend.
- CloudFront forwards requests to the ALB.
- The ALB forwards requests to EC2.
- EC2 processes requests and queries RDS.
- `/api/courses` returns course data through CloudFront.
- AWS WAF is integrated at the CloudFront layer.

Final backend endpoint:

https://d2hvns14tchtf3.cloudfront.net/api/courses

![ALB as CloudFront Origin](images/4-Workshop/4.6-CloudFront/1.png)