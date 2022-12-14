---
title: 'Overview of the architecture'
weight: 73
---

This module demonstrates dynamic parallelism using the Map and Choice states. It contains the following resources:

- Two AWS Lambda functions

- One Amazon Simple Queue Service (Amazon SQS) queue

- One Amazon Simple Notification Service (Amazon SNS) topic

- One Amazon DynamoDB table

- One AWS Step Functions state machine

In this module, Step Functions invokes an AWS Lambda function that retrieves messages from an Amazon SQS queue as a JSON array. A Choice state determines the path of the state machine execution. If there are messages to process, the Choice state passes a JSON array of those messages to a Map state. The Map state iterates through each message in the array dynamically creating separate workflow branches. Each workflow branch writes a message to DynamoDB, and then invokes a second Lambda function to remove the message from Amazon SQS. Finally the branch publishes the message to the Amazon SNS topic.

![Visual Workflow](/static/img/module-5/visual-workflow.png)

Learn more about [Step Functions service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
