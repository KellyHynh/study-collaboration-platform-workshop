---

title: "Test S3 Access from EC2"
date: 2026-09-14
weight: 6
chapter: false
pre: " <b> 4.8.2.6. </b> "

---

# Test S3 Access from EC2

The S3 integration is verified from the EC2 instance using AWS CLI.

#### Step 1: Connect to EC2

SSH into the EC2 instance running the KnoVerse backend.

The terminal should show the EC2 environment, for example:

[ec2-user@ip-172-31-13-175 ~]$

#### Step 2: Verify the IAM Identity

Run:

aws sts get-caller-identity

The expected result contains the IAM Role:

assumed-role/knoverse-ec2-s3-role

This confirms that the EC2 instance is using the expected IAM Role.

#### Step 3: Test Bucket Access

Run:

aws s3 ls s3://knoverse-assets-2026

The expected output includes:

PRE courses/

#### Step 4: Test Object Access

Run:

aws s3 ls s3://knoverse-assets-2026/courses/thumbnails/

The expected output includes the uploaded object:

course-react.png

The successful test demonstrates the following access flow:

EC2
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3 Bucket
 ↓
courses/thumbnails/course-react.png

During the initial test, s3:ListBucket permission was missing, which caused an AccessDenied error when running aws s3 ls against the bucket. The policy was then updated to explicitly include s3:ListBucket at the bucket level. After the update, the bucket and object listing commands completed successfully.

This troubleshooting step confirms that the IAM permissions were tested against an actual EC2-to-S3 operation rather than only being configured in the AWS Console.

Evidence 4.8.2.6: Screenshot of the EC2 terminal showing the AWS CLI commands with successful results.

