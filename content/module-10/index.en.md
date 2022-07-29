---
title: 'Module 10 - Deploy with AWS SAM'
weight: 120
---

The [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/) is an open-source framework for building serverless applications. It provides shorthand syntax to express functions, APIs, databases, and event source mappings. With just a few lines per resource, you can define the application you want and model it using YAML. During deployment, SAM transforms and expands the SAM syntax into AWS CloudFormation syntax, enabling you to build serverless applications faster.

In this module you will use AWS SAM to deploy an application that configures API Gateway to trigger a synchronous Step Functions Express workflow. 