---
title: 'Module 9 - AWS SDK service integrations'
weight: 110
---

AWS Step Functions integrates with many other AWS services. You can use Step Functions [AWS SDK service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/supported-services-awssdk.html) to call over 200 AWS services directly from your state machine, giving you access to over 9,000 API actions.

To use AWS SDK integrations, you specify the service name and API call. Some integrations require parameters and you may optionally specify a service integration pattern. Note that the API action will be camel case, and parameter names will be Pascal case. You can use Amazon States Language to  specify an AWS API action in the Resource field of a task state. To do this, use the following syntax:

`arn:aws:states:::aws-sdk:serviceName:apiAction.[serviceIntegrationPattern]`

**Examples**

- To describe Amazon EC2 instances, use the syntax: `arn:aws:states:::aws-sdk:ec2:describeInstances`. This will return as output the return value of the Amazon EC2 describeInstances API call.

- To list buckets in Amazon S3, use `arn:aws:states:::aws-sdk:s3:listBuckets`. This will return as output the the return value of the Amazon S3 listBuckets API call.

- To start a nested execution in Step Functions use the syntax: `arn:aws:states:::aws-sdk:sfn:startExecution`. You will then add StateMachineArn as a parameter. This will return as output the return value of the Step Functions nested workflow.

