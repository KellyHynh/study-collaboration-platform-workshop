---

title: "Backend Integration Consideration"
date: 2026-09-14
weight: 7
chapter: false
pre: " <b> 4.8.2.7. </b> "

---

# Backend Integration Consideration

The current implementation establishes the infrastructure and secure access path between EC2 and S3.

The complete application-level upload flow can be extended to:

Frontend
   ↓
Backend API
   ↓
EC2
   ↓
IAM Role
   ↓
S3
   ↓
Uploaded Object

When the backend performs an upload, the object can be stored in S3 while the corresponding object key is stored in RDS.

For example:

File:
course-react.png

S3 object key:
courses/thumbnails/course-react.png

RDS:
thumbnailKey =
courses/thumbnails/course-react.png

Direct backend upload integration is not required for the current infrastructure implementation. The current objective is to establish S3, secure it using IAM, attach the IAM Role to EC2, and verify successful EC2-to-S3 access.

