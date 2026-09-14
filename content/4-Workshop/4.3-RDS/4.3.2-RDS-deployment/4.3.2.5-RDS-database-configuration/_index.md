---

title: "Configure Database"
date: 2026-09-14
weight: 5
chapter: false
pre: " <b> 4.3.2.5. </b> "
---

After the RDS instance is ready and the network configuration is complete, the database configuration needs to be prepared for the KnoVerse backend.

#### Database Configuration

Identify the following database connection information:

Database name

Username

Password

Host

Port

The backend configuration can be represented as follows:

DB_HOST=<RDS_ENDPOINT>

DB_PORT=5432

DB_NAME=<DATABASE_NAME>

DB_USER=<DATABASE_USER>

DB_PASSWORD=<DATABASE_PASSWORD>

The actual values should be configured in the backend environment.

**Do not place the actual password in source code, screenshots, or the repository.**
