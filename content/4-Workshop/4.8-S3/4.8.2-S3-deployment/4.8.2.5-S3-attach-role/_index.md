---

title: "Attach IAM Role to EC2"
date: 2026-09-14
weight: 5
chapter: false
pre: " <b> 4.8.2.5. </b> "

---

# Attach IAM Role to EC2

After creating the IAM Role, it must be attached to the EC2 instance running the KnoVerse backend.

#### Step 1: Open EC2

Navigate to:

AWS Console
→ EC2
→ Instances

Select the EC2 instance running the KnoVerse backend.

#### Step 2: Modify IAM Role

Select:

Actions
→ Security
→ Modify IAM role

#### Step 3: Select the Role

For the IAM Role, select:

knoverse-ec2-s3-role

Then click Update IAM role.

The resulting access path is:

EC2
  ↓
knoverse-ec2-s3-role
  ↓
IAM Policy
  ↓
knoverse-assets-2026

This allows the EC2 backend to obtain AWS credentials through the IAM Role without storing long-term AWS credentials in the application source code.

Evidence 4.8.2.5: Screenshot of the EC2 instance showing the attached knoverse-ec2-s3-role.

