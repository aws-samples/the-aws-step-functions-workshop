---
title: 'Implement callback'
weight: 64
---

Navigate to the Lambda service in your account. Search for a function that contains the string `CallbackWithTaskToken`. This is the function that is responsible for processing the events added to the SQS Queue. We'll modify this function to implement a callback.

As you review the code, you'll notice that the Lambda function receives the `TaskToken` from SQS and can return it to the state machine as a parameter in the `.sendTaskSuccess` method.

Uncomment the code that looks like the image below and click the Deploy button.

![Module 4 Workflow](/static/img/module-4/module4-lambda.png)

Now return to your state machine (`WaitForCallbackStateMachine`) and start a new execution.
