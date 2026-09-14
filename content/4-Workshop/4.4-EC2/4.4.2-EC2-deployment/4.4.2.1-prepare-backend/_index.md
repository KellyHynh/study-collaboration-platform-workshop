---

title: "Prepare Backend Application"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.4.2.1. </b> "

---

Before creating the EC2 instance, make sure that the KnoVerse backend application can run normally in the local environment.

#### Check Backend Dependencies

Install the required dependencies:

npm install

After installing the dependencies, start the backend application:

npm start

or use the corresponding command defined in `package.json`.

#### Check Backend API

Test the following API endpoint:

GET /api/courses

The backend should successfully return course data before starting the AWS deployment process.

![Backend API Test](images/4-Workshop/4.4-EC2/2.png)

This helps distinguish application-related issues from problems that may occur during AWS deployment.
