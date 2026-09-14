---

title: "EC2 Overview"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.4.1. </b> "

---

Amazon EC2 is used in the KnoVerse architecture to deploy and operate the backend application on AWS. It provides the compute layer responsible for running the Node.js/Express backend, processing API requests, and communicating with Amazon RDS.

#### 4.4.1.1. Purpose of Using Amazon EC2

Amazon EC2 provides a virtual server on AWS to run the KnoVerse backend.

The backend running on EC2 is responsible for:

- Running the Node.js application.

- Processing HTTP requests.

- Providing REST APIs for the frontend.

- Performing CRUD operations.

- Connecting to and querying data from Amazon RDS.

- Providing an application endpoint for the Application Load Balancer.

After deployment, the backend no longer depends on the developer's local machine to serve the application.

#### 4.4.1.2. Why Choose Amazon EC2?

Amazon EC2 is selected because it allows the backend application to run in a compute environment with relatively full control over the server configuration.

The main reasons include:

- The operating system and instance configuration can be selected according to the application requirements.

- Node.js and the required dependencies can be installed for KnoVerse.

- The application runtime and process can be controlled.

- EC2 can easily connect to RDS within the same VPC.

- EC2 can be integrated with an Application Load Balancer.

- The instance configuration can be expanded or changed as the system grows.

For a learning project such as KnoVerse, EC2 also clearly demonstrates how a backend application can be moved from a local environment to cloud infrastructure.

#### 4.4.1.3. Role in the KnoVerse Architecture

EC2 is positioned between the Application Load Balancer and Amazon RDS in the backend architecture:

![KnoVerse EC2 Architecture](images/4-Workshop/4.4-EC2/1.png)

The main components are:

- CloudFront: distributes and receives requests from clients.

- Application Load Balancer: receives HTTP requests and routes them to the backend.

- EC2: runs the KnoVerse backend.

- RDS: stores PostgreSQL data.

EC2 therefore serves as the application and compute layer of the KnoVerse system.
