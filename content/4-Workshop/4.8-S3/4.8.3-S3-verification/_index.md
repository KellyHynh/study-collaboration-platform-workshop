---

title: "S3 Verification"

date: 2026-09-14

weight: 4

chapter: false

pre: " <b> 4.8.3. </b> "

---

# S3 Verification

After completing the Amazon S3 deployment, the bucket, object access, IAM Role, and EC2-to-S3 connection need to be tested and evaluated.

#### 4.8.3.1. Testing

The S3 implementation was tested at multiple levels:

| **Test** | **Purpose** | **Result** |
| --- | --- | --- |
| Bucket creation | Verify S3 resource | Passed |
| Object upload | Verify object storage | Passed |
| aws sts get-caller-identity | Verify EC2 IAM Role | Passed |
| aws s3 ls | Verify bucket access | Passed |
| Object listing | Verify object access | Passed |

The final test confirmed that the EC2 backend environment could access the KnoVerse S3 bucket using the attached IAM Role.

#### 4.8.3.2. Security Considerations

The S3 bucket uses Block Public Access, preventing direct public access to the bucket and its objects.

Access from EC2 is controlled through:

EC2
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3

The policy follows the principle of least privilege by granting only the required S3 operations and limiting access to the KnoVerse bucket.

Long-term AWS access keys and secret keys are not hard-coded into the backend source code.

#### 4.8.3.3. Result

Amazon S3 has been successfully added as the object-storage layer of KnoVerse. The current implementation establishes and verifies the EC2-to-S3 access infrastructure. Application-level upload handling through the backend remains a future extension.

The implementation successfully demonstrates:

1. Creation of a dedicated S3 bucket.
2. Configuration of private bucket access.
3. Organization of course assets using S3 prefixes.
4. Upload of a course thumbnail object.
5. Creation of an EC2-specific IAM Role.
6. Configuration of limited S3 permissions.
7. Attachment of the IAM Role to the EC2 backend instance.
8. Successful verification of the IAM identity from EC2.
9. Successful access to the S3 bucket and uploaded object from EC2.

S3 complements RDS rather than replacing it: RDS stores structured application data, while S3 stores file-based objects and assets.

![ALB as CloudFront Origin](/images/4-Workshop/4.8-S3/1.png)