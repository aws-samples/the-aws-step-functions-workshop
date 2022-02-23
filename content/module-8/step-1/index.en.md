---
title: 'Overview of the concept'
weight: 101
---

AWS Step Functions integrates with AWS services, letting you call each service's API actions from your workflow. You can use Step Functions' AWS SDK integrations to call any of the over 200 AWS services directly from your state machine, giving you access to over 9,000 API actions.

To use AWS SDK integrations, you specify the service name and API call, and, optionally, a service integration pattern. Note that the API action will always be camel case, and parameter names will be Pascal case. For example, you could use Step Functions' **startSyncExecution** API action and specify the parameter **StateMachineArn**. You can call AWS SDK services directly from the Amazon States Language in the Resource field of a task state. To do this, use the following syntax:

`arn:aws:states:::aws-sdk:serviceName:apiAction.[serviceIntegrationPattern]`

For example, for Amazon EC2, you might use `arn:aws:states:::aws-sdk:ec2:describeInstances`. This would return output as defined for the Amazon EC2 describeInstances API call.

For Amazon S3, if you want to list buckets you might use `arn:aws:states:::aws-sdk:s3:listBuckets` which uses the `listBuckets` API call.
