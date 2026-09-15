---
title: "Cost Estimation and Optimization"
date: 2026-09-15
weight: 9
chapter: false
pre: " <b> 4.9. </b> "
---

# Cost Estimation and Optimization

This section estimates the monthly and annual operating cost of the AWS infrastructure used to deploy the KnoVerse application.

The estimate is intended for a small-scale learning and internship environment rather than a production workload. The main objective is to identify the expected cost of keeping the deployed system running continuously and to demonstrate how the architecture can be optimized to reduce unnecessary AWS spending.

All amounts below are approximate USD estimates. Actual charges depend on the AWS Region, resource configuration, traffic, storage, requests, Free Tier or promotional credits, and the actual time each resource remains active. The final estimate should be verified using the AWS Pricing Calculator before deployment or before presenting the final cost. AWS Pricing Calculator provides monthly and 12-month estimates based on the workload assumptions entered by the user.

## 4.9.1. Cost Estimation Assumptions

The estimate uses the following simplified workload:

- AWS Region: ap-southeast-1 (Asia Pacific – Singapore)
- One small Amazon EC2 instance running the KnoVerse backend.
- One small Amazon RDS for PostgreSQL instance.
- One Application Load Balancer.
- One Amazon CloudFront distribution.
- One AWS WAF Web ACL with a small number of rules.
- One Amazon S3 bucket for application assets.
- One AWS Amplify application for the frontend.
- Low development/testing traffic.
- Approximately 730 hours of operation per month.
- Small amounts of storage and data transfer.
- No paid AWS Support Plan included.
- No domain registration cost included.
- Taxes are not included.

Because the project is intended for learning and demonstration, the estimated workload is substantially smaller than a production system serving a large number of users.

## 4.9.2. Estimated AWS Services Cost

### Amazon EC2

The EC2 instance hosts the Node.js/Express backend of KnoVerse.

Estimated configuration:

- 1 small general-purpose EC2 instance
- Approximately 730 running hours/month
- Linux operating system
- Small EBS volume for the application and operating system

Estimated monthly cost:

- EC2 compute: approximately $8.00–$9.00/month
- EBS storage: approximately $1.00–$2.00/month

Estimated EC2 subtotal: approximately $10.00/month.

The actual price depends on the selected instance type and EBS configuration.

### Amazon RDS for PostgreSQL

Amazon RDS hosts the PostgreSQL database used by KnoVerse.

Estimated configuration:

- 1 small RDS PostgreSQL instance
- Approximately 730 hours/month
- Small general-purpose storage volume
- Single-AZ deployment for the learning environment
- No Multi-AZ configuration

Estimated monthly cost:

- DB instance: approximately $12.00–$14.00/month
- Database storage: approximately $1.00–$2.00/month

Estimated RDS subtotal: approximately $14.00/month.

Using a small Single-AZ instance is an important cost optimization for an internship project. Multi-AZ deployment would provide higher availability but would increase the cost significantly.

### Application Load Balancer

The Application Load Balancer distributes HTTP/HTTPS traffic to the backend EC2 instance.

For a low-traffic development environment, the estimated cost is approximately:

- ALB hourly charge and low-volume LCU usage: approximately $18.00–$20.00/month

Estimated ALB subtotal: approximately $19.00/month.

The actual ALB cost depends on the number of Load Balancer Capacity Units (LCUs) consumed.

### Amazon CloudFront

CloudFront is used as the public distribution layer in front of the backend ALB.

For a low-traffic learning workload, an estimated usage of approximately 5 GB of data transfer and a small number of requests results in a relatively low usage-based charge.

Estimated monthly cost:

- CloudFront requests and data transfer: approximately $0.50/month

Estimated CloudFront subtotal: approximately $0.50/month.

AWS also provides a Free flat-rate CloudFront plan for eligible use cases. The selected pricing model should therefore be checked before final deployment because the cost structure can differ from traditional pay-as-you-go pricing.

### AWS WAF

AWS WAF protects the public application endpoint from common web attacks.

Estimated configuration:

- 1 Web ACL
- A small number of rules
- Low request volume

Estimated monthly cost:

- Web ACL: approximately $5.00/month
- Rules and request processing: approximately $1.00/month

Estimated WAF subtotal: approximately $6.00/month.

The actual WAF charge depends on the number of Web ACLs, rules, and web requests.

### Amazon S3

S3 is used for application assets and other stored objects.

Estimated workload:

- Approximately 5 GB of Standard storage
- Low request volume
- Small amount of data transfer

Estimated monthly cost:

- Storage: approximately $0.12/month
- Requests and related usage: approximately $0.05/month

Estimated S3 subtotal: approximately $0.17/month.

### AWS Amplify

Amplify hosts the KnoVerse frontend application.

For a small development application with limited build minutes, storage, requests, and data transfer, the expected usage can remain within the applicable Free Tier or credits for an eligible account.

For a conservative estimate outside applicable Free Tier benefits:

- Build and hosting usage: approximately $0.50/month

Estimated Amplify subtotal: approximately $0.50/month.

The exact amount depends on build minutes, stored data, requests, and data transfer.

### Other Supporting Costs

Other possible costs may include:

- Data transfer between AWS services: approximately $0.50/month for the small workload assumed here.
- CloudWatch logs and monitoring: approximately $0.50/month.
- Elastic IP or other optional networking charges: approximately $0.00–$1.00/month depending on configuration.

Estimated supporting-services subtotal: approximately $1.00/month.

## 4.9.3. Monthly Cost Summary

Based on the assumptions above, the estimated monthly cost is:

| AWS Service | Estimated Monthly Cost |
|---|---:|
| Amazon EC2 + EBS | $10.00 |
| Amazon RDS PostgreSQL | $14.00 |
| Application Load Balancer | $19.00 |
| Amazon CloudFront | $0.50 |
| AWS WAF | $6.00 |
| Amazon S3 | $0.17 |
| AWS Amplify | $0.50 |
| Data Transfer + CloudWatch + other supporting usage | $1.00 |
| **Estimated Total** | **$51.17/month** |

Estimated annual cost:

$51.17 × 12 = **$614.04/year**

This is a planning estimate for keeping the infrastructure available continuously for approximately 730 hours per month. It should not be interpreted as a guaranteed AWS bill.

## 4.9.4. Free Tier and Credit Consideration

The actual amount paid by the project can be considerably lower if the AWS account is eligible for Free Tier benefits or AWS promotional credits.

For example, AWS states that new customers can receive AWS Free Tier credits under the current Free Tier program. These credits can be applied to eligible services. Therefore, the estimated infrastructure cost and the actual amount charged to the account may differ.

The report should distinguish between:

- Estimated infrastructure cost before credits.
- Applicable Free Tier benefits.
- AWS promotional credits.
- Actual amount charged to the AWS account.

For this reason, the AWS Billing and Cost Management dashboard should be checked during and after deployment.

## 4.9.5. Cost Optimization

Several design decisions were made to keep the KnoVerse deployment suitable for an internship and learning environment.

### 1. Use small compute instances

The backend does not require a large EC2 instance because the expected workload is low. A small instance is sufficient for running the Node.js/Express API.

### 2. Use Single-AZ RDS

The database uses a Single-AZ configuration for the learning environment. Multi-AZ is useful for higher availability but is unnecessary for a small demonstration system and would increase the cost.

### 3. Keep storage requirements small

The project stores only the data and assets required by the application. Unnecessary backups, logs, and temporary files should be removed regularly.

### 4. Use CloudFront caching

CloudFront can cache appropriate responses and reduce the number of requests that reach the origin. This can improve performance and reduce origin traffic.

### 5. Monitor WAF rules and requests

Only the required WAF rules should be enabled. Unnecessary rules and excessive logging should be avoided because WAF and logging costs depend on usage.

### 6. Stop or delete resources after testing

Resources that are not required outside development or demonstration periods should be stopped or removed when possible.

In particular, continuously running EC2 and RDS instances can become the main recurring costs of the architecture.

### 7. Monitor AWS billing

AWS Billing and Cost Management should be checked regularly. Budget alerts can be configured to notify the developer when spending reaches a predefined threshold.

## 4.9.6. Cost Comparison: Always-On vs. Workshop Usage

The estimated $51.17/month assumes that the main infrastructure remains available continuously.

For an internship project, the resources may not need to run 24 hours a day.

If the backend EC2 and RDS resources are only used during development, testing, and demonstrations, the effective monthly cost can be significantly lower. However, services such as ALB and some networking components may continue to generate charges while they remain provisioned.

Therefore, a practical cost-saving strategy is to:

1. Start the required resources before development or demonstration.
2. Perform testing and verification.
3. Stop resources that support stopping.
4. Delete temporary resources that are no longer needed.
5. Review the AWS Billing dashboard after the work is completed.

## 4.9.7. Final Cost Assessment

The proposed KnoVerse AWS architecture is estimated at approximately:

- **Monthly infrastructure cost:** $51.17/month
- **Estimated 12-month cost:** $614.04/year
- **Hardware cost:** $0 additional, because the deployed application uses cloud infrastructure and no additional physical hardware is required for the AWS deployment.
- **AWS Free Tier / promotional credits:** may reduce the actual amount charged.

The largest recurring costs in this architecture are expected to come from Amazon RDS, the Application Load Balancer, and Amazon EC2. Therefore, these resources should receive the highest priority during cost optimization.

The estimate demonstrates that the architecture is technically feasible for a small-scale internship project, while also showing that keeping the complete infrastructure running continuously is more expensive than a minimal development environment. For this reason, resource scheduling, right-sizing, monitoring, and removal of unused resources are important parts of the deployment process.

## 4.9.8. AWS Pricing Calculator

The final estimate should be verified using the AWS Pricing Calculator with the actual resource specifications and Region used in the deployment.

AWS Pricing Calculator:
https://calculator.aws/

The calculator can be used to generate monthly and 12-month estimates, review the calculation behind each service, and compare different infrastructure configurations.

The values in this section are therefore presented as a practical planning estimate rather than a fixed AWS invoice amount.
