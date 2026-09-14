---

title: "Amazon Amplify Overview"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.7.1. </b> "

---

# Amazon Amplify Overview

#### 4.7.1.1. Role in the KnoVerse Architecture

Amazon Amplify is used to deploy and host the frontend of the KnoVerse system.

The KnoVerse frontend is developed as a web application and stored in a repository. Amplify connects to this repository to perform the build and deployment process, then provides a public URL for users to access the application.

In the overall architecture, Amplify is responsible for the frontend layer:

Amplify

&nbsp;&nbsp;↓

Frontend
![ALB as CloudFront Origin](images/4-Workshop/4.7-Amplify/1.png)

Amplify focuses on frontend hosting and deployment, while the backend and database are deployed on other AWS services.

#### 4.7.1.2. Why Choose Amazon Amplify

Amazon Amplify is selected for the KnoVerse frontend because it provides a relatively simple web application deployment process and fits a development model based on a Git repository.

The main benefits include:

- Direct integration with the source code repository.
- Automatic build and deployment when source code is updated.
- A production URL for the frontend.
- Environment variable management.
- Less need to configure a web server for the frontend manually.
- Suitability for project development and demonstration.

Within KnoVerse, Amplify separates the frontend from the EC2 backend, allowing each component to be deployed and managed independently.

