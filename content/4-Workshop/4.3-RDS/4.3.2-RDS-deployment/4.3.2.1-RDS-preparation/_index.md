---

title: "Preparation and Requirements"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.3.2.1. </b> "

---

Before creating the Amazon RDS instance, the basic database and networking requirements need to be identified.

#### Database and Network Requirements

The following information is used for the KnoVerse RDS deployment:

| **Component**   | **Value**                    |
| --------------- | ---------------------------- |
| Database Engine | PostgreSQL                   |
| AWS Region      | ap-southeast-1               |
| VPC             | KnoVerse VPC                 |
| Database Port   | 5432                         |
| Application     | KnoVerse Backend             |
| Database Client | PostgreSQL-compatible client |

These values provide the basic configuration required for deploying the PostgreSQL database and connecting it with the KnoVerse backend.

#### Required Information

Before creating the RDS database, prepare the following information:

- Database name.

- Master username.

- Master password.

- Database schema.

- Database seed/demo data if required.

- Security Group for the database.

The database credentials should be prepared in advance and stored securely. The actual password should not be included directly in the source code, screenshots, or repository.
