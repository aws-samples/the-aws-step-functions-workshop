---
title: 'Review definition'
weight: 63
---

Callback tasks provide a way to pause a workflow until a task token is returned. A task might need to wait for a human approval, integrate with a third party, or call legacy systems. For tasks like these, you can pause Step Functions indefinitely, and wait for an external process or workflow to complete. For these situations Step Functions allows you to pass a task token to the service integration. The task will pause until it receives that task token back with a `SendTaskSuccess` or `SendTaskFailure` call.

To see a list of what integrated services support waiting for a task token (`.waitForTaskToken`), see [Optimized integrations for Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).

Although the callback logic is initially implemented in the ASL definition, the callback is not yet being executed in the Lambda function that processes the SQS messages.

State machine definition:
![Module 4 Workflow](/static/img/module-4/code.png)
