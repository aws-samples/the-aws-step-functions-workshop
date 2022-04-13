---
title: 'Execute initial workflow'
weight: 63
---

Navigate to [Step Functions in the console](https://console.aws.amazon.com/states/home) and click the state machine that begins with **"WaitForCallbackStateMachine"**. The application architecture for this module is displayed in the diagram below. This state machine sends message to SQS using **Wait for Callback** and passes a task token. SQS then sends the message and the token to a Lambda function. However, the callback (step #3 in diagram below) is not yet implemented in the Lambda function. 

![Module 4 architecture](/static/img/module-4/callback-architecture.png)

Execute the state machine now using the default input. Notice that the execution will become paused indefinitely at the `Start Task and Wait For Callback` state.

![Module 4 Workflow](/static/img/module-4/initial-workflow.png)
