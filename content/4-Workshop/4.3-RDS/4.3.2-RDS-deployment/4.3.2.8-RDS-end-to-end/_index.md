---

title: "End-to-End Verification"
date: 2026-09-14
weight: 8
chapter: false
pre: " <b> 4.3.2.8. </b> "
---

This step verifies that the complete database deployment works from the application to RDS.

The verification flow is:

![RDS End-to-End Flow](images/4-Workshop/4.3-RDS/image10.png)

#### Step 1 — Check Backend

Make sure the backend running on EC2 is operating normally.

#### Step 2 — Send API Request

Send a request to the following endpoint:

GET /api/courses

#### Step 3 — Check Response

The API should return an HTTP success response and course data.

For example:

HTTP/1.1 200 OK

Content-Type: application/json

#### Step 4 — Compare with Database

Verify that the data returned by the API corresponds to the data stored in RDS.

If the API successfully returns course data, the following flow can be confirmed:

Backend

↓

Database connection

↓

RDS PostgreSQL

↓

Database query

↓

API response

The complete flow is working end-to-end.

![RDS Verification Result](images/4-Workshop/4.3-RDS/11.png)

