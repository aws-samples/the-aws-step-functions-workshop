---
title: 'Implement callback'
weight: 65
---

Navigate to the [Lambda service in the console](https://console.aws.amazon.com/lambda/home) and find the function that contains the string **CallbackWithTaskToken**. This is the function that is responsible for processing the messages added to the SQS queue. You will modify this function to implement a callback.

Review the code and notice that the Lambda function receives the `TaskToken` from SQS and can return it to the state machine as a parameter in the `.sendTaskSuccess` method.

Uncomment the code indicated in the image below and click the **Deploy** button.

![Module 4 Workflow](/static/img/module-4/lambda.png)


