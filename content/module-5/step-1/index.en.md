---
title: 'Overview of the concept'
weight: 71
---

This sample project demonstrates dynamic parallelism using a Map and Choice state. This sample project creates the following:

- Two AWS Lambda functions

- An Amazon Simple Queue Service (Amazon SQS) queue

- An Amazon Simple Notification Service (Amazon SNS) topic

- An Amazon DynamoDB table

- An AWS Step Functions state machine

In this project, Step Functions uses an AWS Lambda function to pull messages off an Amazon SQS queue, and pass a JSON array of those messages to a Map state. For each message in the queue, the state machine writes the message to DynamoDB, invokes another Lambda function to remove the message from Amazon SQS, and then publishes the message to the Amazon SNS topic.

![Visual Workflow](/static/ExtraModule-visual-workflow.png)

For more information on Map states, Choice states and Step Functions service integrations, see the following:

Visit [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) to explore Map state.

Visit [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) to explore Choice state.

Visit [Using AWS Step Functions with other services](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html) for Step Functions service integrations
