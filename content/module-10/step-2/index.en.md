---
title: 'Overview of the concept'
weight: 101
---

This module demonstrates how to use Step Functions to run a batch job with **error-handling**, with various state types, using AWS Batch and Amazon SNS. Deploying this module will create an AWS Step Functions state machine, an AWS Batch job, and an Amazon SNS topic.

- Learn more about [AWS Batch job Optimized integrations](https://docs.aws.amazon.com/step-functions/latest/dg/connect-batch.html).

- Learn more about [Amazon SNS topic Optimized integrations](https://docs.aws.amazon.com/step-functions/latest/dg/connect-sns.html).

- Learn more about [Step Functions service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).


In this module, Step Functions uses a state machine to call the AWS Batch job **synchronously**. It then waits for the job to **succeed or fail**, **retries** and **catches errors when a job fails**, then sends an Amazon SNS topic with a message about whether the job succeeded or failed.

![Flowchart](/static/img/module-10/error-handling-module10-1.png)