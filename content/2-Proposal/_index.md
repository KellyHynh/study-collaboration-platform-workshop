---

title: "Proposal"

date: 2026-06-01

weight: 2

chapter: false

pre: " <b> 2. </b> "

---

## STUDY COLLABORATION PLATFORM

### 1. Project Overview

The project is a web-based study collaboration platform designed to provide a centralized environment for users to create, manage, and access learning content.

The platform focuses on common study activities such as creating courses, organizing learning materials, managing lessons, and interacting with course-related content. The project is initially designed as a small-scale web application but is deployed using AWS services to gain practical experience with cloud infrastructure, application deployment, storage, networking, monitoring, and scalability.

The project also serves as a practical demonstration of how a traditional web application can be gradually migrated from a local development environment to a cloud-based architecture using managed AWS services.

### 2. Objectives

The main objectives of the project are:

* Build a functional web-based study collaboration platform.
* Implement the core frontend and backend features of the application.
* Design and implement a relational database for application data.
* Deploy the application using AWS services.
* Gain practical experience with cloud infrastructure and AWS service integration.
* Apply AWS services to different aspects of the application, including computing, database, storage, content delivery, networking, and monitoring.
* Understand the differences between developing an application locally and operating it in a cloud environment.
* Practice basic cloud security, resource management, monitoring, and cost optimization.

The project will primarily focus on practical AWS implementation rather than building a highly complex production-scale system.

### 3. Problem Statement

### What's the Problem?

Managing learning materials and study content across different tools can make it difficult to organize courses, lessons, and related resources in one place.

From a technical perspective, developing the application only in a local environment does not provide sufficient experience with cloud deployment, infrastructure configuration, networking, monitoring, and managed services.

Therefore, the project aims to combine the development of a functional web application with practical AWS implementation.

### The Solution

The proposed solution is a centralized web application where users can manage and access learning content through a structured course-based system.

The application uses a backend API to handle business logic and communicate with a relational database. Amazon RDS is used for persistent application data, while Amazon S3 is used for file and asset storage.

The application backend is deployed on Amazon EC2. Application traffic can be distributed through an Application Load Balancer, while Amazon CloudFront is used for content delivery and caching.

Amazon CloudWatch is used to monitor the deployed infrastructure and application environment.

Additional AWS services such as ElastiCache, AWS Lambda, API Gateway, and AWS Amplify are explored during development to understand alternative architectures and potential future improvements.

### 4. Solution Architecture

The proposed architecture combines compute, database, storage, networking, content delivery, and monitoring services.

The main application flow is:

* Users access the web application through the frontend.
* CloudFront provides content delivery and caching where appropriate.
* Application traffic is routed to the backend through the Application Load Balancer.
* The backend application runs on Amazon EC2.
* EC2 communicates with Amazon RDS for persistent application data.
* Amazon S3 stores uploaded files and application assets.
* Amazon CloudWatch collects monitoring information and application-related logs.
* IAM controls permissions between users, applications, and AWS resources.
* VPC provides the networking environment for the AWS infrastructure.

The architecture will be refined during development based on practical requirements, cost considerations, and deployment constraints.

![Final Project AWS Architecture](/images/2-Proposal/platform_architecture.PNG)

### AWS Services Used

* **Amazon EC2**: Hosts and runs the backend application.
* **Amazon RDS**: Provides the relational database for persistent application data.
* **Amazon S3**: Stores uploaded files and application assets.
* **Amazon CloudFront**: Provides content delivery and caching.
* **Application Load Balancer**: Distributes incoming application traffic and provides health checks.
* **Amazon VPC**: Provides the networking environment for the AWS resources.
* **Amazon CloudWatch**: Provides monitoring, metrics, and logs.
* **AWS IAM**: Manages permissions and access to AWS resources.
* **Amazon ElastiCache**: Explored for caching frequently accessed application data.
* **AWS Lambda**: Explored as a serverless computing alternative.
* **Amazon API Gateway**: Explored for exposing serverless APIs.
* **AWS Amplify**: Explored as an alternative approach for frontend hosting and deployment.

### Component Design

* **Frontend**: Provides the user interface for managing and accessing learning content.
* **Backend**: Provides REST APIs and handles application business logic.
* **Database**: Amazon RDS stores structured application data such as courses, lessons, and related information.
* **File Storage**: Amazon S3 stores application files and uploaded resources.
* **Compute**: Amazon EC2 runs the backend application.
* **Networking**: Amazon VPC and security groups control network communication between application components.
* **Load Balancing**: Application Load Balancer manages incoming application traffic and performs health checks.
* **Content Delivery**: CloudFront provides caching and delivery of supported application content.
* **Monitoring**: CloudWatch provides infrastructure metrics and logs.
* **Security**: IAM is used to control access to AWS resources according to the principle of least privilege.

### 5. Timeline

The project is planned over a 12-week period.

* **Weeks 1-3: AWS Fundamentals**

  * Learn basic AWS concepts and service categories.
  * Study and practice S3, RDS, EC2, and basic AWS infrastructure.
  * Become familiar with AWS Console and CLI.

* **Weeks 4-7: AWS Service Exploration**

  * Practice S3 and CloudFront integration.
  * Learn VPC, Application Load Balancer, and CloudWatch.
  * Apply AWS services to a small web application.
  * Explore Lambda, API Gateway, ElastiCache, and Redis.

* **Week 8: Project Planning**

  * Define project requirements and scope.
  * Design the database structure.
  * Design the initial system and AWS architecture.
  * Prepare the development environment.

* **Week 9: Backend and Database Development**

  * Implement the main backend structure.
  * Set up the project database.
  * Develop the main APIs and CRUD operations.
  * Integrate the backend with Amazon RDS.

* **Week 10: Core Feature Development**

  * Implement the main application features.
  * Integrate frontend and backend components.
  * Implement Amazon S3 functionality.
  * Continue testing the application's core workflows.

* **Week 11: Integration and Testing**

  * Complete the remaining core features.
  * Integrate the main application components.
  * Perform functional testing.
  * Fix bugs and prepare the project for deployment.

* **Week 12: AWS Deployment**

  * Deploy the backend to Amazon EC2.
  * Configure RDS and S3 for the deployed application.
  * Configure Application Load Balancer and CloudFront.
  * Configure CloudWatch monitoring.
  * Perform final deployment testing.
  * Complete AWS architecture and deployment documentation.

### 6. Budget Estimation

The project is designed to minimize infrastructure costs by using AWS Free Tier-eligible resources where available and shutting down or removing unnecessary resources after testing.

The actual cost depends on resource usage, deployment duration, data transfer, storage, and the AWS account's applicable Free Tier eligibility.

The main cost categories include:

* Amazon EC2: Compute resources for running the backend application.
* Amazon RDS: Managed relational database instance.
* Amazon S3: Storage for application files and assets.
* CloudFront: Content delivery and data transfer.
* Application Load Balancer: Load balancing and traffic processing.
* CloudWatch: Monitoring, metrics, and logs.
* Other services: Potential experimental usage of ElastiCache, Lambda, API Gateway, or Amplify.

Cost management will be performed throughout the project by monitoring AWS usage, removing unused resources, and reviewing estimated costs before enabling additional services.

### 7. Risk Assessment

#### Risk Matrix

* **Unexpected AWS Costs**: Medium impact, medium probability.
* **Deployment Configuration Errors**: Medium impact, medium probability.
* **Database Connectivity Issues**: Medium impact, medium probability.
* **Application Bugs During Deployment**: Medium impact, medium probability.
* **AWS Resource or Service Configuration Issues**: Medium impact, low probability.
* **Limited Development Time**: High impact, medium probability.

#### Mitigation Strategies

* Monitor AWS resource usage regularly.
* Use AWS cost monitoring and budget alerts where appropriate.
* Remove unused resources after experiments and testing.
* Use security groups and IAM permissions carefully.
* Keep the application configuration separate from source code using environment variables.
* Test application components locally before deploying them to AWS.
* Back up important project data and maintain version control.
* Deploy and test AWS components incrementally instead of configuring the entire infrastructure at once.

#### Contingency Plans

If a specific AWS service causes unexpected complexity or cost, the architecture can be simplified while maintaining the core functionality of the project.

The application can also continue to be developed and tested locally if a cloud resource becomes temporarily unavailable or requires reconfiguration.

### Expected Outcomes

At the end of the project, the expected outcomes are:

* A functional web-based study collaboration platform.
* A working backend API and relational database.
* Successful deployment of the application on AWS.
* Practical experience with EC2, RDS, S3, CloudFront, VPC, ALB, and CloudWatch.
* Basic understanding of IAM, ElastiCache, Lambda, API Gateway, and Amplify.
* A documented AWS architecture and deployment process.
* Practical experience with cloud infrastructure, monitoring, security, and cost management.

The final project will demonstrate not only the development of a functional web application but also the ability to design, deploy, monitor, and manage an application using multiple AWS services.
