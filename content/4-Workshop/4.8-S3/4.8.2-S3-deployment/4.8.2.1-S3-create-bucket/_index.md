---

title: "Create S3 Bucket"
date: 2026-09-14
weight: 1
chapter: false
pre: " <b> 4.8.2.1. </b> "

---

# Create S3 Bucket

The first step is to create an S3 bucket for KnoVerse assets.

#### Step 1: Open Amazon S3

1. Sign in to the AWS Management Console.
2. Open Amazon S3.
3. Select Buckets from the navigation panel.
4. Click Create bucket.

#### Step 2: Configure Bucket Type

For Bucket type, select:

General purpose

A General Purpose bucket is sufficient for the KnoVerse object-storage use case.

#### Step 3: Configure Bucket Name

Enter a globally unique bucket name.

The bucket used in this implementation is:

knoverse-assets-2026

#### Step 4: Configure Object Ownership

Keep the default object ownership configuration:

Bucket owner enforced

This keeps ACLs disabled and allows bucket policies and IAM permissions to control access.

#### Step 5: Configure Public Access

Keep Block all public access enabled.

Block Public Access
☑ Block all public access

The bucket is not intended to be directly accessible from the public Internet. Access will instead be controlled through the EC2 IAM Role.

#### Step 6: Configure Encryption

Use the default Amazon S3 server-side encryption:

Server-side encryption:
SSE-S3

For the current implementation, S3 Bucket Key is left disabled because an additional KMS-based configuration is not required for this use case.

#### Step 7: Create the Bucket

Review the configuration and click:

Create bucket

After creation, the bucket appears in the S3 bucket list.

Expected result:

knoverse-assets-2026

Evidence 4.8.2.1: Screenshot of the created bucket and its configuration, including bucket type, Block Public Access, and encryption settings.

