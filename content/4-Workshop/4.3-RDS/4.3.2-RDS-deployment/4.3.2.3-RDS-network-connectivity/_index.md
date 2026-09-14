---

title: "Configure Network and Connectivity"
date: 2026-09-14
weight: 3
chapter: false
pre: " <b> 4.3.2.3. </b> "
---


After creating the database, the network configuration needs to be identified and verified so that the backend running on EC2 can connect to RDS.

#### Step 1 — Open Connectivity & Security

In the RDS database, open:

**Connectivity & security**

Check the following information:

- VPC.

- Availability Zone.

- Subnet.

- Security Group.

- Endpoint.

- Port.

The database endpoint has a format similar to:

<database-identifier>.<random-id>.<region>.rds.amazonaws.com

The default PostgreSQL port is:

5432

#### Step 2 — Identify the Endpoint

The endpoint will be used as **DB_HOST** in the backend.

For example:

DB_HOST=<RDS_ENDPOINT>

DB_PORT=5432

![RDS Connectivity and Endpoint](images/4-Workshop/4.3-RDS/image5.png)

