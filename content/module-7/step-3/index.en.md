---
title: 'Overview of the architecture'
weight: 93
---

This module contains the following resources:

- Three AWS Lambda functions
- One API Gateway endpoint
- One AWS IAM Role used to integrate API Gateway with Step Functions

In this module, you will create an Express workflow that receives an array of integers as input, and in parallel calculates the sum, the average, and the maximum and minimum values. The state machine returns a JSON object with the responses from each of the parallel tasks.

Next, you will set up an asynchronous API Gateway integration with your state machine. You will execute the state machine by sending a request to API Gateway. You will then modify the integration to make the response from Step Functions synchronous.
![Visual Workflow](/static/img/module-7/visual-workflow.png)


