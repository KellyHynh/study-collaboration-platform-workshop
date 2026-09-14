---

title: "Configure Security Group"
date: 2026-09-14
weight: 4
chapter: false
pre: " <b> 4.3.2.4. </b> "
---

The Security Group controls traffic to the RDS instance and determines which resources are allowed to establish database connections.

#### Step 1 — Open Security Group

From the **Connectivity & security** section, open the Security Group associated with the RDS instance.

#### Step 2 — Configure Inbound Rule

Add an inbound rule for PostgreSQL:

Type:

PostgreSQL

Protocol: TCP

Port: 5432

Source: Security Group of the backend EC2

When the EC2 Security Group is used as the source, RDS only allows resources associated with that Security Group to establish database connections.

The database port should not be opened to all sources.

Do not use:

0.0.0.0/0

for PostgreSQL in a real deployment environment.

#### Step 3 — Check Outbound Rules

Make sure the outbound configuration does not prevent the required connections.

![RDS Security Group](/images/4-Workshop/4.3-RDS/image6.png)

