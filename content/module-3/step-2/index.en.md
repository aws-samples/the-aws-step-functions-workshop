---
title: 'Execute asynchronous task'
weight: 52
---

In this module we will implement a synchronized task orchestration pattern called [Run a Job (.sync)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-sync). With this pattern, Step Functions will call a service integration and wait until its job is complete before advancing to the next state. To see a list of the integrated services that support synchronization, see [Optimized integrations for Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).

Navigate to [Step Functions in the console](https://console.aws.amazon.com/states/home) and click the state machine that starts with **"BatchJobNotification"**. This workflow submits an AWS Batch job. In its initial state the job is asynchronous. The state machine submits the job to the AWS Batch service but does not wait for the job to complete. Instead, it immediately moves to the next state and sends a Notify Success message to an Amazon SNS topic.

Here is what the initial workflow looks like:

![Module 3 Workflow](/static/img/module-3/initial-workflow.png)

Here is what the Task definition looks like for the AWS Batch job. Take note of the Resource node.

![Module 3 Code](/static/img/module-3/initial-code.png)

Now click **Start execution** and use the default input. The AWS Batch service performs a job, which may take minute or more to finish. Notice how quickly this execution completes.

![Initial graph](/static/img/module-3/initial-graph.png)

Now imagine that we need our state machine to stay synchronized with AWS Batch and only to proceed once the job is complete. 
