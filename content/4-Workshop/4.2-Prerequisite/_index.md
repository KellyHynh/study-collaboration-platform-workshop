---

title: "Prerequisite"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.2. </b> "

---

# Prerequisite

Before beginning the AWS deployment, the required cloud account, development environment, application source code, database configuration, and access permissions should be prepared. The following prerequisites define the environment used throughout the KnoVerse deployment workshop.

## 4.2.1. AWS Account and Billing

An active AWS account is required to provision and configure the cloud resources used in this workshop.

The AWS account should have:

* Access to the AWS Management Console.
* Permission to create and configure the required AWS resources.
* A valid billing configuration or applicable AWS credits.
* Access to the AWS Free Tier where applicable.

Because several AWS resources may incur charges while they are running, AWS billing and resource usage should be monitored throughout the deployment process. Resources that are no longer required should be stopped or removed after the workshop to avoid unnecessary costs.

## 4.2.2. AWS Region

All primary AWS resources used in the KnoVerse deployment are provisioned in the following AWS Region:

**Region:** `ap-southeast-1`

**Region name:** Asia Pacific (Singapore)

Using a consistent Region simplifies resource management and network connectivity between services such as Amazon EC2, Amazon RDS, and Application Load Balancer.

The selected Region should be confirmed before creating resources because some AWS resources and configurations are Region-specific.

## 4.2.3. IAM Access and Permissions

An AWS identity with sufficient permissions is required to create, configure, and manage the resources used throughout the workshop.

The required access covers the following AWS services and resource categories:

* Amazon EC2
* Amazon RDS
* Amazon VPC
* Elastic Load Balancing
* Amazon CloudFront
* AWS WAF
* Amazon S3
* AWS Amplify
* AWS Identity and Access Management (IAM), where required for service configuration

For learning and workshop purposes, an account with broad administrative permissions may be used to simplify resource provisioning. In a production environment, permissions should instead follow the **principle of least privilege**, granting only the access required for each operation.

The AWS root account should not be used for routine deployment activities.

## 4.2.4. Development Environment

The local development environment should provide the tools required to prepare, test, and deploy the KnoVerse application.

### Required Tools

* Git
* Node.js
* npm
* Visual Studio Code or another code editor
* Web browser
* Terminal or PowerShell

### AWS Tools

* AWS Management Console
* AWS CLI

The AWS Management Console is used for configuring and monitoring AWS resources throughout the workshop, while AWS CLI may be used for command-line verification and resource management.

## 4.2.5. Application Source Code

The KnoVerse source code must be available before beginning the deployment.

The application consists of two primary components:

```text
KnoVerse
├── Frontend
└── Backend
```

The frontend should be able to build successfully in the local development environment and communicate with the backend API.

The backend should be able to:

* Run on Node.js.
* Expose the required REST API endpoints.
* Connect to a PostgreSQL database.
* Receive environment-specific configuration through environment variables.
* Run successfully in the local environment before deployment.

Local functionality should be verified before introducing AWS infrastructure so that deployment issues can be distinguished from application-level issues.

## 4.2.6. Database Prerequisites

Before deploying Amazon RDS, the database structure and required configuration should be prepared.

The following items should be available:

* PostgreSQL database schema.
* Required tables and relationships.
* Database migrations or initialization scripts.
* Seed or demonstration data where applicable.
* Database credentials.
* Backend database configuration.

Database connection information should be provided through environment variables rather than hard-coded directly into the application source code.

Typical configuration includes:

```text
DB_HOST
DB_PORT
DB_NAME
DB_USER
DB_PASSWORD
```

Sensitive credentials should not be committed to the source code repository.

## 4.2.7. Network Prerequisites

The AWS deployment requires a network environment capable of supporting communication between the Internet-facing components, backend application, and database.

The deployment uses the following networking components:

* Amazon VPC
* Subnets
* Route Tables
* Internet Gateway
* Security Groups
* Network ACL
* Application Load Balancer

These components provide the underlying network connectivity and traffic control required by the KnoVerse architecture.

The detailed configuration and relationship between these components are described in the networking and deployment sections later in the workshop.

## 4.2.8. AWS CLI Configuration

AWS CLI is optional for the deployment process when resources are configured through the AWS Management Console. However, it can be used to verify the AWS account and perform command-line operations.

After installation, the AWS CLI configuration can be verified using:

```bash
aws sts get-caller-identity
```

This command confirms the AWS identity currently being used by the CLI and helps prevent deployment operations from being performed in the wrong AWS account.

## 4.2.9. Infrastructure-as-Code Tools

Infrastructure-as-Code tools such as **AWS SAM, AWS CDK, and Terraform** are not required for this workshop.

The KnoVerse deployment focuses on understanding and implementing AWS infrastructure through the AWS Management Console, with command-line tools used where appropriate for verification.

These Infrastructure-as-Code tools are mentioned as optional alternatives for future automation and reproducibility of the infrastructure configuration.

## 4.2.10. AWS Cost Awareness

Before provisioning AWS resources, the potential cost of the deployed infrastructure should be considered.

The workshop uses AWS services that may generate charges depending on account eligibility, resource configuration, and usage. Therefore, the following practices are recommended:

* Check applicable AWS Free Tier or credit usage.
* Monitor AWS billing information during deployment.
* Avoid unnecessarily running resources after testing.
* Stop or delete resources that are no longer required.
* Review the deployed resources before ending the workshop.

Cost monitoring is particularly important for compute, database, load balancing, networking, and other usage-based AWS resources.


