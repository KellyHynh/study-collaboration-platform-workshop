---

title: "Connect EC2 to Amazon RDS"

date: 2026-09-14

weight: 8

chapter: false

pre: " <b> 4.4.2.8. </b> "

---

After the environment variables are configured, the backend running on EC2 connects to RDS.

The connection flow is:

EC2

 │

 │ TCP 5432

 ▼

RDS PostgreSQL

#### Connection Checklist

Check the following:

- RDS is in the **Available** state.

- The RDS endpoint is correct.

- Port 5432 is allowed.

- The EC2 Security Group and RDS Security Group allow the required traffic.

- Database credentials are correct.

After the connection is successful, the backend can perform database queries.

