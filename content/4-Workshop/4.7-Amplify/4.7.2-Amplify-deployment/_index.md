---

title: "Amazon Amplify Deployment"

date: 2026-09-14

weight: 2

chapter: false

pre: " <b> 4.7.2. </b> "

---

# Amazon Amplify Deployment

This section describes the complete process of deploying the KnoVerse frontend to Amazon Amplify.

#### 4.7.2.1. Prepare the Frontend Application

Before deployment, the KnoVerse frontend needs to:

- Have complete source code.
- Have a repository containing the source code.
- Build successfully locally.
- Have the required API endpoints clearly identified.

For local development, the frontend can use the Vite development server and proxy:

server: {
    proxy: {
        "/api": {
            target: "http://localhost:3000",
            changeOrigin: true,
        },
    },
},

For production deployment, the frontend needs to use the backend endpoint deployed on AWS instead of depending on localhost.

#### 4.7.2.2. Create the Amplify Application

Open AWS Management Console -> Amplify.

Choose the option to create or host a web application and connect it to the repository containing the KnoVerse source code.

Select:

1. Git provider.
2. Project repository.
3. Branch to deploy.

The production branch is:

main

#### 4.7.2.3. Configure Build Settings

Amplify needs to know how to install dependencies and build the frontend.

For an application using Vite, the build process includes:

Install dependencies
        ↓
Run build command
        ↓
Generate production files
        ↓
Deploy generated files

The project build command needs to correspond to the configuration in `package.json`.

For example:

npm run build

After a successful build, the frontend production files are deployed by Amplify.

#### 4.7.2.4. Configure Environment Variables

Different development and production configuration values can be defined through Amplify Environment Variables.

An example is:

API_BASE_URL

The production application can use the AWS endpoint instead of:

http://localhost:3000

Environment variables separate configuration from source code and make it easier to switch between environments.

In the KnoVerse deployment, environment variables are checked at:

Amplify -> App -> Environment variables

Do not place secrets or sensitive credentials directly in frontend environment variables because values used by the frontend may become part of the client-side application.

#### 4.7.2.5. Deploy the main Branch

After completing the configuration, start the deployment.

Amplify performs:

Source Code
    ↓
Clone Repository
    ↓
Install Dependencies
    ↓
Build
    ↓
Deploy
    ↓
Production Hosting

Monitor the deployment status in Amplify. A successful status indicates that deployment has completed.

#### 4.7.2.6. Check the Production URL

After deployment, Amplify provides a production URL.

The current KnoVerse production application address is:

https://main.d2hfdjfyze730o.amplifyapp.com/

Expected results:

- The website displays normally.
- Frontend pages are accessible.
- No build or deployment errors appear.
- The frontend can make API requests to the AWS backend.

#### 4.7.2.7 Frontend – Backend Connectivity Check

Frontend deployment is
only considered complete when the frontend can communicate with the
production backend.

Request architecture:
![ALB as CloudFront Origin](/images/4-Workshop/4.7-Amplify/image.png)

Frontend performs a
request to the API:

`/api/courses`

The backend processes
the request and retrieves course data from RDS.

The data is then
returned to the frontend for display.

The actual results of
KnoVerse show that the production website can successfully load **course
data**.

This is important
evidence because it demonstrates that the **production frontend has successfully
communicated with the AWS backend**, rather than only proving that the Amplify
website can be opened.

#### 4.7.2.8. Verification from a Different Network Environment

To verify that the
application does not depend on the local environment, the production URL can
be accessed from another device or network.

Example:

Device A

```
│

└── Production Internet

         ↓

      Amplify

         ↓

      AWS Backend
```

If the website can
still be accessed and display course data, the deployment has achieved its
public accessibility objective.

