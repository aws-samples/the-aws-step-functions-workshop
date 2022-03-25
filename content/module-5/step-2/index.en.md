---
title: 'Overview of the concept'
weight: 71
---

This module demonstrates dynamic parallelism using the Map and Choice states. This modules contains the following resources:

- Two AWS Lambda functions

- One Amazon Simple Queue Service (Amazon SQS) queue

- One Amazon Simple Notification Service (Amazon SNS) topic

- One Amazon DynamoDB table

- One AWS Step Functions state machine

In this project, Step Functions invokes an AWS Lambda function that retrieves messages from an Amazon SQS queue. The Lambda function then returns a JSON array of those messages to a Map state. The Map state iterates through each message in the array dynamically creating separate workflow branches. Each workflow branch writes a message to DynamoDB, and then invokes a second Lambda function to remove the message from Amazon SQS. Finally the branch publishes the message to the Amazon SNS topic.

![Visual Workflow](/static/img/module-5/ExtraModule-visual-workflow.png)

For more information read the documentation below.

- Learn more about the [Map state](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html).

- Learn more about the [Choice state](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html).

- Learn more about [Step Functions service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
