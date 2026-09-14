---

title: "Configure Environment Variables"

date: 2026-09-14

weight: 7

chapter: false

pre: " <b> 4.4.2.7. </b> "

---

The backend needs to be configured with environment variables appropriate for the AWS environment.

In particular, the database configuration must point to Amazon RDS instead of the local PostgreSQL database.

For example:

DB_HOST=<RDS_ENDPOINT>

DB_PORT=5432

DB_NAME=<DATABASE_NAME>

DB_USER=<DATABASE_USER>

DB_PASSWORD=<DATABASE_PASSWORD>

Other application configuration values should also be configured according to the deployment environment.

Do not put passwords or secrets directly into the source code.
