---

title: "RDS Verification"
date: 2026-09-14
weight: 4
chapter: false
pre: " <b> 4.3.3. </b> "
---

After completing the Amazon RDS deployment, the database needs to be tested and evaluated to ensure that it works correctly with the KnoVerse backend.

#### 4.3.3.1. Connection and Functionality Testing

The main tests include:

| **Test**                | **Expected Result**         |
| ----------------------- | --------------------------- |
| EC2 → RDS               | Connection successful       |
| PostgreSQL port 5432    | Accessible from the backend |
| Database authentication | Successful                  |
| Database query          | Returns data                |
| Backend → RDS           | Successful                  |
| GET /api/courses        | HTTP 200 OK                 |
| Course data             | Correct data returned       |

These tests help verify that the database layer is working correctly before continuing with the integration of other AWS services.

#### 4.3.3.2. Configuration Evaluation

After deployment, the RDS configuration should be evaluated based on:

- Database availability.

- Network connectivity.

- Security Group configuration.

- Storage configuration.

- Compute configuration.

- Database accessibility.

- Application compatibility.

For the workshop environment, the configuration is selected to remain simple and cost-effective while still meeting the requirements of KnoVerse.

#### 4.3.3.3. Troubleshooting

During the cloud database deployment process, several issues may occur.

**EC2 → RDS connection failed**

Check the following items in order:

1. RDS has an Available status.

2. EC2 and RDS have compatible network configurations.

3. The RDS Security Group allows TCP port 5432.

4. The inbound rule source allows the backend EC2 Security Group.

5. Database credentials are correct.

6. The RDS endpoint is correct.

**Backend still uses the local database**

Check the backend environment variables and make sure:

DB_HOST

is pointing to the RDS endpoint instead of localhost.

**API does not return data**

Check:

- Database schema.

- Seed data.

- Database connection.

- SQL queries.

- Backend logs.

#### 4.3.3.4. Optimization Options

As the KnoVerse system grows, RDS can be optimized according to actual requirements.

Possible improvements include:

- Adjusting the DB instance class.

- Increasing or optimizing storage.

- Configuring appropriate backups.

- Using Multi-AZ for higher availability requirements.

- Optimizing database indexes and queries.

- Monitoring database metrics using Amazon CloudWatch.

- Using a caching layer such as Amazon ElastiCache when the application needs to reduce database load.

These options do not necessarily need to be implemented in the basic workshop. They are considered future expansion options for the system.

#### 4.3.3.5. Results

After completing the deployment, Amazon RDS has taken responsibility for the database layer of KnoVerse.

The main results are:

- The PostgreSQL database is deployed on Amazon RDS.

- The database is integrated with the system VPC.

- The Security Group controls database traffic.

- The backend running on Amazon EC2 can connect to RDS.

- The KnoVerse database schema and data are initialized.

- The backend can perform database queries.

- The /api/courses endpoint successfully returns course data.

- The database layer operates together with the application layer on AWS.

The architecture after completing the RDS deployment is illustrated below:

![RDS Architecture](images/4-Workshop/4.3-RDS/image1.png)

