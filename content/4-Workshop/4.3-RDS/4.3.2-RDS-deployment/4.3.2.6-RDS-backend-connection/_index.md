---

title: "Connect RDS with Backend"
date: 2026-09-14
weight: 6
chapter: false
pre: " <b> 4.3.2.6. </b> "
---

After configuring RDS, the KnoVerse backend running on EC2 needs to be updated to use the RDS database configuration.

#### Before Deployment

The backend uses the local PostgreSQL database:

Backend

│

▼

Local PostgreSQL

#### After Deployment

The backend running on EC2 connects to the PostgreSQL database on RDS:

Backend on EC2

│

▼

RDS PostgreSQL

The backend uses the RDS endpoint instead of:

localhost

or the database host of the local environment.

After updating the database configuration, restart the backend to apply the new database connection.

![Backend RDS Configuration](images/4-Workshop/4.3-RDS/image7.png)

