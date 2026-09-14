---

title: "Create EC2 Instance"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.4.2.2. </b> "

---

This section describes the process of creating the EC2 instance that will run the KnoVerse backend application.

#### Step 1 — Open Amazon EC2

In the AWS Management Console, navigate to:

Services → EC2 → Instances → Launch instance

Make sure the selected Region is:

ap-southeast-1

![Open Amazon EC2](images/4-Workshop/4.4-EC2/3.png)

#### Step 2 — Set Instance Name

Set a name that makes the instance easy to identify.

For example:

knoversee-backend

#### Step 3 — Select Operating System

Select an Amazon Machine Image (AMI) that is suitable for the backend application.

For this workshop, Amazon Linux can be used.

#### Step 4 — Select Instance Type

Select an instance type that is suitable for the project's workload and the available AWS Free Tier or credits.

For a development or demo environment, a small instance should be preferred to reduce costs.

#### Step 5 — Create Key Pair

Create or select an EC2 Key Pair that will be used to connect to the instance through SSH.

The private key must be stored securely.

Do not commit the private key file to the Git repository.

#### Step 6 — Configure Network Settings

Select:

- KnoVerse VPC.

- An appropriate subnet.

- A suitable Public IP configuration for accessing the EC2 instance.

The Security Group will be configured separately to allow the required traffic.

#### Step 7 — Launch the Instance

Review the configuration and select:

**Launch instance**

Wait until the instance changes to the **Running** state and the system status checks are completed.

![EC2 Network Settings](images/4-Workshop/4.4-EC2/4.png)
