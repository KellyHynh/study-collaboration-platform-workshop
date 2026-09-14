---

title: "Amplify Verification"

date: 2026-09-14

weight: 3

chapter: false

pre: " <b> 4.7.3. </b> "

---

# Amplify Verification

#### 4.7.3.1. Deployment Testing

After deployment, perform the following checks:

| **Item** | **Expected Result** |
| --- | --- |
| Production URL | Accessible successfully |
| Frontend rendering | Displays normally |
| Static assets | Loads successfully |
| API request | Successful |
| Course data | Displays correctly |
| Backend connection | Operational |
| Database data | Retrieved successfully |

#### 4.7.3.2. API Communication Testing

Check the request:

GET /api/courses

The request needs to pass through:

Amplify
   ↓
CloudFront
   ↓
ALB
   ↓
EC2
   ↓
RDS

The backend ALB endpoint was verified to return HTTP 200 OK and course data. The production frontend also successfully displayed the course data. This proves that the frontend -> backend -> database pipeline is working end-to-end.

#### 4.7.3.3. Testing After EC2 Restart

The Node.js backend was initially run directly with:

node src/server.js

This process depends on the terminal or SSH session. When the terminal closes, the Node.js process may stop:

Node.js stopped
      ↓
ALB health check failed
      ↓
Target = unhealthy
      ↓
CloudFront API request failed
      ↓
Frontend cannot load course data

The backend was subsequently configured to use PM2 for process management.

The goal is:

EC2
 ↓
PM2
 ↓
Node.js Backend
 ↓
ALB

PM2 allows the backend to continue running when the SSH session closes and can be configured to automatically restart the process when EC2 reboots.

#### 4.7.3.4. Evaluate the Results

After deployment, Amazon Amplify has fulfilled its role as the frontend hosting service for KnoVerse.

Achieved results:

- The frontend was successfully deployed to AWS.
- The production URL is accessible from the Internet.
- The frontend displays the correct interface.
- The frontend can call the production backend.
- Course data is successfully retrieved from the backend system.
- Amplify is separated from the backend infrastructure.
- Deployment can be managed through a Git-based workflow.

Frontend/backend architecture after deployment:

Frontend

&nbsp;&nbsp;↓

Amplify

&nbsp;&nbsp;↓

CloudFront

&nbsp;&nbsp;↓

ALB

&nbsp;&nbsp;↓

EC2

&nbsp;&nbsp;↓

RDS

![ALB as CloudFront Origin](/images/4-Workshop/4.7-Amplify/1.png)