---

title: "Amazon RDS Overview"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.3.1. </b> "

---

# Amazon RDS Overview

#### 4.3.1.1. Purpose of Using Amazon RDS

Amazon Relational Database Service (Amazon RDS) is used in KnoVerse to provide a managed PostgreSQL database environment on AWS.

During the initial development stage, the KnoVerse backend uses PostgreSQL on the local machine. When deploying the system to AWS, the database is migrated to Amazon RDS so that the backend application running on Amazon EC2 can access the database through the AWS network.

The main objectives of deploying Amazon RDS are:

- Move the KnoVerse database to the cloud environment.
- Separate the database from the application server.
- Allow the backend running on EC2 to access the database through a private network.
- Maintain the application's existing data structure and database schema.
- Provide a foundation for managing and scaling the database within the AWS environment.

#### 4.3.1.2. Why Choose Amazon RDS?

Amazon RDS is selected instead of installing and managing PostgreSQL directly on an EC2 instance.

The main reasons include:

**Managed service:** AWS manages many tasks related to the database infrastructure, reducing the amount of manual database administration required.

**AWS integration:** Amazon RDS operates within an Amazon VPC and can communicate with other AWS resources through appropriate networking and security configurations.

**PostgreSQL support:** KnoVerse uses PostgreSQL as its database engine, making Amazon RDS for PostgreSQL compatible with the application's existing database environment.

**Application and database separation:** The backend can run on EC2 while the database is managed separately by RDS. This provides a clear separation between the application layer and the database layer.

**Scalability:** Amazon RDS provides options to modify compute capacity, storage, and database configurations as the system grows in the future.

#### 4.3.1.3. Role in the KnoVerse Architecture

After the AWS infrastructure is deployed, Amazon RDS is responsible for the **database layer** of the KnoVerse system.

The main connection architecture is illustrated below:

![KnoVerse RDS Architecture](/images/4-Workshop/4.3-RDS/image1.png)

The backend does not access the database through CloudFront or the Application Load Balancer. Requests from clients are first handled by the backend application running on EC2. The backend then performs database operations with Amazon RDS through the configured AWS network.

This separation allows the application and database layers to be managed independently while maintaining controlled communication between the two components.
