---
title: 'Module 10 - Deploy with AWS CDK'
weight: 120
---

The [AWS Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/v2/guide/home.html) lets you build applications in the cloud with the power of a programming language. The AWS CDK supports TypeScript, JavaScript, Python, Java, C#/.Net, and (in developer preview) Go. Developers can use one of these supported programming languages to define reusable cloud components known as [Constructs](https://docs.aws.amazon.com/cdk/v2/guide/constructs.html). You compose these together into [Stacks](https://docs.aws.amazon.com/cdk/v2/guide/stacks.html) and [Apps](https://docs.aws.amazon.com/cdk/v2/guide/apps.html).

![AWS CDK diagram](/static/img/module-10/AppStacks.png)

In this module you will use AWS CDK with TypeScript to deploy an application that configures API Gateway to trigger a synchronous Step Functions Express workflow. 