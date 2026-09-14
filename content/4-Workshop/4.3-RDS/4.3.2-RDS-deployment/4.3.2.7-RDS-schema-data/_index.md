---

title: "Initialize Schema and Data"
date: 2026-09-14
weight: 7
chapter: false
pre: " <b> 4.3.2.7. </b> "
---

After the backend can connect to RDS, the KnoVerse database schema can be initialized.

#### Step 1 — Connect to RDS PostgreSQL

Use a PostgreSQL client or an appropriate database tool to connect to the RDS endpoint.

#### Step 2 — Create Database Structure

Run the KnoVerse database migration or schema initialization script.

![Initialize RDS Database](/images/4-Workshop/4.3-RDS/image8.png)

#### Step 3 — Check Tables

Verify that all required tables have been created successfully.

#### Step 4 — Import Data

If the workshop uses sample data, seed or import the data into the database.

#### Step 5 — Check Relationships

Verify the following database relationships and constraints:

- Primary keys.

- Foreign keys.

- Unique constraints.

- Relationships between tables.

![RDS Database Tables](/images/4-Workshop/4.3-RDS/image9.png)

