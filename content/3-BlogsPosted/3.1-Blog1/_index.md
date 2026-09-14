---

title: "Blog 1"

date: 2026-09-13

weight: 1

chapter: false

pre: " <b> 3.1. </b> "

---

# Automate CI/CD Troubleshooting with AWS DevOps Agent and GitHub

For those who have worked with GitHub Actions or CI/CD systems, you have probably encountered this familiar situation:

* Push code to GitHub.
* The CI/CD pipeline fails.
* Open the logs to find the error.
* Go through the Build, Test, or Deploy steps one by one.
* Modify the code.
* Create a Pull Request.
* Wait for review and run the pipeline again.

For a few repositories, this process is not too complicated. However, in systems with many projects, multiple workflows, and hundreds of deployments every day, manually analyzing logs can consume a significant amount of development team's time.

In a recent AWS Blog post, I came across **AWS DevOps Agent**, an AI Agent designed to automatically investigate the root cause of pipeline failures and assist in creating Pull Requests to fix the issues. What I find interesting is that AWS is not only applying AI to assist with programming, but also bringing AI directly into the DevOps workflow.

## How Does AWS DevOps Agent Work?

According to the architecture introduced by AWS, when a GitHub Actions Workflow fails, the system can automatically trigger the AWS DevOps Agent through a Webhook.

The overall workflow can be summarized as:

**Developer Push Code → GitHub Actions → Pipeline Failed → Webhook → AWS DevOps Agent → Read Workflow Logs, Source Code, Commit History, and CloudWatch Logs → Analyze Root Cause → GitHub MCP Server → Create Pull Request**

Instead of requiring a DevOps Engineer or Software Engineer to manually inspect each log step, the AI Agent can perform the investigation process similarly to an experienced engineer.

## Role of Each Component

### 1. GitHub App

The GitHub App provides Read-only access so that the AI Agent can:

* Read source code.
* Read Workflow Logs.
* Check commit history.
* Track deployments.

This allows the Agent to understand what changed before the failure occurred.

### 2. Amazon CloudWatch

CloudWatch provides logs from applications running on AWS.

In a situation where the deployment pipeline completes successfully but the application still fails to start, CloudWatch can contain important information that helps the AI Agent investigate the root cause.

For example:

* A required Secret cannot be found.
* Required IAM permissions are missing.
* Runtime errors occur.
* The application crashes.

### 3. GitHub MCP Server

One interesting aspect is that the GitHub App only provides the AI with access to read data.

To allow the AI to perform actions such as:

* Create a Branch.
* Update files.
* Create a Pull Request.
* Push code.

AWS uses a **GitHub MCP (Model Context Protocol) Server** as a bridge that allows the Agent to write changes back to GitHub after determining a potential solution.

## A Practical Example

AWS provides an example involving a TypeScript error.

A developer adds a `trackingId` property to an Object, but the corresponding Interface does not define this property.

As a result, the Build step fails.

Instead of simply reporting:

`TS2353`

`Object literal may only specify known properties...`

AWS DevOps Agent can:

* Read the Build logs.
* Open the specific file causing the error.
* Check the Interface definition.
* Identify the commit that introduced the change.
* Analyze the root cause.
* Suggest a fix.
* Create a Pull Request for the developer to review.

This can significantly reduce the time required to investigate CI/CD failures.

## What I Find Interesting

After reading the article, what impressed me the most was not the fact that AI can create a Pull Request.

What is more interesting is that AWS is building a more complete CI/CD troubleshooting workflow:

* The system detects the failure.
* AI investigates the root cause.
* AI proposes a solution.
* Humans review the changes before merging.

This still maintains the **Human-in-the-loop** approach, meaning that the AI does not directly modify the source code without review. The generated Pull Request still needs to be reviewed and approved by a developer.

In my opinion, this is a reasonable approach because it takes advantage of AI while maintaining human control over code quality and system safety.

## Best Practices from AWS

AWS also provides several recommendations when implementing this approach:

* Apply the **Least Privilege** principle to the GitHub App and Personal Access Token.
* Only enable the permissions that the AI actually needs.
* Always require human review before merging a Pull Request.
* Monitor Agent activities through Amazon CloudWatch.
* Authenticate Webhooks using HMAC to prevent forged requests.

These are important principles for maintaining security while introducing more automation into the development workflow.

## Conclusion

In my opinion, AWS DevOps Agent demonstrates an interesting direction for the future of DevOps.

Previously, AI was mainly used to assist developers with writing code. Now, AI is beginning to participate in more parts of the software development lifecycle, including monitoring CI/CD pipelines, analyzing logs, identifying failure causes, and proposing Pull Requests to resolve issues.

Although this technology cannot completely replace the role of DevOps Engineers or Software Engineers, it can significantly reduce the time spent troubleshooting failures and allow technical teams to focus more on developing new features.

![AWS DevOps Agent Architecture](/images/3-BlogsPosted/blog1.png)
## Reference

**AWS Blog:**
[AWS DevOps Agent and GitHub CI/CD Troubleshooting](https://aws.amazon.com/vi/blogs/mt/automate-ci-cd-troubleshooting-with-aws-devops-agent-and-github/?fbclid=IwY2xjawUTrv9wZG9mAWV4dG4DYWVtAjEwAGJyaWQRMUlSbHJNYTFyZ25OVXRySzlzcnRjBmFwcF9pZBAyMjIwMzkxNzg4MjAwODkyAAEeK5VwKabHemtPovw3AsP3aBI7kLFROu1OC4KgnJY3DQaO56vyO7bxCPGKiTQ_aem_6a_p6f8MRgNteopw3DcC9Q)

