---
title: 'Overview of the concept'
weight: 92
---

This module demonstrates how to configure a state machine that executes parallel workflow branches using the Parallel state. It also shows how to trigger the execution of a state machine from API Gateway. This module contains the following resources:

- Three AWS Lambda functions
- One API Gateway
- One AWS IAM Role used to integrate API Gateway with Step Functions

In this module, you will create an Express Workflow that receives an array of integers as input, and in parallel calculates the sum, the average, and the maximum and minimum values. The state machine returns a JSON object with the responses from each of the parallel tasks.

Next, you will set up an asynchronous API Gateway integration with your state machine. You will execute the state machine by sending a request to API Gateway. You will then modify the integration to make the response from Step Functions synchronous.
![Visual Workflow](/static/img/module-7/visual-workflow.png)

For more information on Parallel states visit [Parallel States](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-parallel-state.html)

For more information about the API Gateway integration types visit [API Gateway Integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-integration-types.html)
