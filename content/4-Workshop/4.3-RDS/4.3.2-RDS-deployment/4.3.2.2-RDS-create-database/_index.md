---

title: "Create PostgreSQL Database on Amazon RDS"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 4.3.2.2. </b> "
---

This section describes the process of creating a PostgreSQL database on Amazon RDS for the KnoVerse backend.

#### Step 1 — Open Amazon RDS

Access the AWS Management Console and open **Amazon RDS**.

Make sure the selected Region is:

Asia Pacific (Singapore)

ap-southeast-1

![Open Amazon RDS](/images/4-Workshop/4.3-RDS/image2.png)

#### Step 2 — Create the Database

Select:

**Databases → Create database**

Choose the deployment method appropriate for the workshop.

#### Step 3 — Select the Database Engine

Under Engine options:

Engine type:

PostgreSQL

Select a PostgreSQL version that is compatible with the application.

If the local database uses a specific PostgreSQL version, selecting a compatible version helps reduce potential migration issues.

![RDS Connectivity and Endpoint](/images/4-Workshop/4.3-RDS/image3.png)

#### Step 4 — Configure Database Credentials

Configure:

- DB instance identifier.

- Master username.

- Master password.

The password must be stored securely and should not be placed directly in the source code.

#### Step 5 — Configure Compute and Storage

Select an instance class and storage configuration appropriate for the workshop.

For a learning or demo environment, a small configuration that fits the available Free Tier or AWS credits should be preferred.

#### Step 6 — Create the Database

Review the configuration and select:

**Create database**

Wait until the database changes to the available state.

![RDS Connectivity and Endpoint](/images/4-Workshop/4.3-RDS/image4.png)
