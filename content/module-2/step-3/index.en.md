---
title: 'Review workflow'
weight: 43
---

Navigate to [Step Functions in the console](https://console.aws.amazon.com/states/home) and click the state machine that starts with **"RequestResponseStateMachine"**. In this sample app we will wait for a specified delay, then we will publish to a SNS topic using the Request Response pattern.

Step Functions will call the service API for the resource defined (using the `resource` string) in your task state. Step Functions will wait for an HTTP response from the service API and then immediately progress to the next state. This called the Request Response pattern.

If the service API starts an asynchronous job Step Functions will not wait for that job to complete. You can learn more about how to start and poll the results of asynchronous jobs in Module 3.

Review the definition in Workflow Studio:

![Module 2 Workflow](/static/img/module-2/workflow.png)

Notice the `"Resource"` string of the task state below. This code designates a Request Response service integration pattern.

![Module 2 Code](/static/img/module-2/code.png)
