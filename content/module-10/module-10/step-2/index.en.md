---
title: 'Overview of the concept'
weight: 101
---

This sample project demonstrates how to use Step Functions to run a batch job with **error-handling**, with various state types, using AWS Batch and Amazon SNS. Deploying this sample project will create an AWS Step Functions state machine, an AWS Batch job, and an Amazon SNS topic.

In this project, Step Functions uses a state machine to call the AWS Batch job synchronously. It then waits for the job to succeed or fail, retries and catches errors when a job fails, then sends an Amazon SNS topic with a message about whether the job succeeded or failed.



