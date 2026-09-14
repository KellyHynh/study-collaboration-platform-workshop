---

title: "Create IAM Policy"
date: 2026-09-14
weight: 4
chapter: false
pre: " <b> 4.8.2.4. </b> "

---

# Create IAM Policy

The S3 bucket should not be accessed by the EC2 backend using hard-coded AWS access keys. Instead, the backend uses an IAM Role.

The required permissions are limited to:

s3:ListBucket
s3:GetObject
s3:PutObject
s3:DeleteObject

#### Step 1: Open IAM

Navigate to:

AWS Console
→ IAM
→ Roles
→ Create role

#### Step 2: Select Trusted Entity

Under Trusted entity type, select:

AWS service

For the service/use case, select:

EC2

This creates a trust relationship allowing EC2 instances to assume the role.

The resulting trust relationship contains:

{
  "Effect": "Allow",
  "Action": "sts:AssumeRole",
  "Principal": {
    "Service": "ec2.amazonaws.com"
  }
}

#### Step 3: Create the Permission Policy

Create an inline policy for the role. The policy separates bucket-level and object-level permissions because s3:ListBucket applies to the bucket itself, while object operations apply to objects inside the bucket.

The policy used is:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "KnoVerseS3BucketAccess",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::knoverse-assets-2026"
    },
    {
      "Sid": "KnoVerseS3ObjectAccess",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::knoverse-assets-2026/*"
    }
  ]
}

The first statement provides access to the bucket:

arn:aws:s3:::knoverse-assets-2026

The second statement provides access to objects inside the bucket:

arn:aws:s3:::knoverse-assets-2026/*

This avoids granting unrestricted S3 access such as:

s3:*

#### Step 4: Name the Role

The IAM Role is named:

knoverse-ec2-s3-role

Description:

IAM role for EC2 backend to access KnoVerse S3 assets.

#### Step 5: Create the Role

Review:

- Trusted entity: EC2
- S3 permissions: limited to knoverse-assets-2026
- Role name: knoverse-ec2-s3-role

Then select Create role.

Evidence 4.8.2.4: Screenshot showing the IAM Role, EC2 trusted entity, and S3 permissions.

