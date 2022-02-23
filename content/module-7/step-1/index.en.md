---
title: 'Overview of the concept'
weight: 91
---

This sample project demonstrates how to create a state machine that executes activities in parallel using a Parallel state. It also explains how to trigger the execution of a state machine from API Gateway. This sample project creates the following:

- Three AWS Lambda functions
- An API Gateway to integrate with your State Machine
- An AWS IAM Role to make the integration between API Gateway and Step Functions

In this project, you will create an Express State Machine that receives an array of data values, and in parallel calculates the Sum of the values, the Average of the values, and the Maximum & Minimum values. The State Machine returns a JSON object with the aggregated response of the three functions executed in parallel.

Finally, you will setup an API Gateway integration (integration type AWS) to start the execution of the State Machine from API Gateway and you will be able to tweak your integration to make the response from Step Functions synchronous.
![Visual Workflow](/static/module-7-visual-workflow.png)

For more information on Parallel states visit [Parallel States](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-parallel-state.html)

For more information about the API Gateway integration types visit [API Gateway Integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-integration-types.html)
