---

title: "Blog 2"

date: 2026-09-13

weight: 2

chapter: false

pre: " <b> 3.2. </b> "

---

# Building AI Agents for Domain-Specific Classification at Scale

Hello everyone! When talking about AI, many people may immediately think of ChatGPT or chatbots that can answer questions. However, the current AI trend is gradually moving toward a new concept: **AI Agents** — AI systems that can not only generate answers but also analyze data, use tools, make decisions, and explain the reasoning behind those decisions.

In a recent AWS Blog post, I learned about how AWS built an AI Agent system specifically for **domain-specific classification** by combining Amazon Bedrock with serverless AWS services. What I find interesting is that this problem is not only about AI, but also demonstrates how AWS can build an architecture that is scalable, easy to manage, and applicable to different industries.

## The Problem AWS Is Trying to Solve

In many fields such as healthcare, finance, and the public sector, data often exists in the form of free-form text. These documents need to be classified into standardized codes or categories for reporting, statistics, or regulatory compliance.

Previously, this work was mainly performed manually or through rule-based systems. However, as the amount of data increases and regulations change frequently, these approaches gradually reveal limitations in terms of processing speed, scalability, and operational costs.

This is why AWS proposes building an AI Agent that can automatically analyze data, retrieve additional information when necessary, and provide classification results together with explanations.

## How Is an AI Agent Different from a Chatbot?

A traditional chatbot receives a question and generates an answer based on the knowledge of the language model.

An AI Agent, on the other hand, can perform multiple steps before producing a result, such as:

* Analyze the input data.
* Retrieve information from trusted sources.
* Combine and evaluate the results.
* Make a decision together with a **Confidence Score**.
* Explain the reasoning and record the entire processing workflow.

This ability to perform **reasoning** and **tool use** is what creates the key difference between an AI Agent and a traditional chatbot.

## The Proposed AWS Architecture

In the article, AWS builds the system using a serverless architecture with several familiar services:

* **Amazon S3** stores the input data.
* **Amazon EventBridge** detects when new data is uploaded.
* **AWS Lambda** processes and splits the data.
* **Amazon SQS** manages queues for asynchronous processing.
* **Amazon Bedrock** provides AI models for the reasoning process.
* **Amazon DynamoDB** stores classification results together with the reasoning process and references.
* **Amazon CloudWatch** monitors the performance, cost, and activities of the AI Agent.

Instead of processing all the data on a single server, this architecture takes advantage of serverless services to automatically scale as the data volume increases.

## How the System Works

The processing workflow can be summarized as follows:

1. The user uploads data to Amazon S3.
2. EventBridge detects the event and triggers Lambda.
3. Lambda divides the data into smaller groups and places them into Amazon SQS.
4. Another Lambda function reads each group of data and sends a request to the AI Agent.
5. The AI Agent uses Amazon Bedrock to perform the reasoning process and can also call additional tools such as web search or Amazon Bedrock Knowledge Bases to retrieve information before producing a result.
6. The result is stored in DynamoDB with information such as:

   * Classification Code
   * Description
   * Confidence Score
   * Reasoning process
   * Reference sources
7. CloudWatch records metrics such as processing time, the number of tokens used, and costs to support system monitoring and optimization.

One notable aspect of this architecture is that the AI does not only return the final result but also records the entire reasoning process. This helps improve transparency and supports investigation when necessary.

## What I Find Most Interesting

After reading the article, what impressed me was not the use of a new AI model, but rather how AWS designed the entire processing workflow.

Instead of simply allowing AI to generate an answer, the system also focuses on important factors in enterprise environments, such as:

* Scalability through a serverless architecture.
* Transparency through reasoning and reference sources.
* Audit Trail for each decision.
* Performance and cost monitoring through CloudWatch.

In my opinion, these factors are important for applying AI in fields that require a high level of reliability, such as healthcare, finance, and the public sector.

## Conclusion

AI Agents are opening up a new approach to building AI applications on cloud platforms. Instead of only acting as chatbots, AI systems can now analyze data, use tools, retrieve information, explain decisions, and assist people in handling more complex problems.

Through this article, I realized that combining **Amazon Bedrock** with serverless services such as **Lambda, SQS, DynamoDB, and EventBridge** can not only help build a scalable AI system but also meet requirements for transparency, governance, and operation in real-world environments.

This is a very interesting direction for anyone learning about AI on AWS, especially as AI Agents are becoming an emerging trend in the technology industry.

![Domain-Specific Classification Architecture](images/3-BlogsPosted/blog2.png)

## Reference

**AWS Blog:**

[Building AI agents for domain-specific classification at scale](https://aws.amazon.com/vi/blogs/publicsector/building-ai-agents-for-domain-specific-classification-at-scale/?fbclid=IwY2xjawUTseBwZG9mAWV4dG4DYWVtAjEwAGJyaWQRMUlSbHJNYTFyZ25OVXRySzlzcnRjBmFwcF9pZBAyMjIwMzkxNzg4MjAwODkyAAEePI-I1hySd2uaqr3S4zH3-fVZZJWDoGgvvdlYX-6PjofPQvqLBL7VgR-yAuU_aem_cZYA-3tPQyL9WXPVIzO-Ig)