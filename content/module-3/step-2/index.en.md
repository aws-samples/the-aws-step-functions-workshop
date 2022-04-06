---
title: 'Execute initial workflow'
weight: 52
---

In this module we will implement the Sync Polling pattern. With Sync Polling, Step Functions will call a service integration and wait until its job is complete before advancing to the next state.

Find the state machine in your account that starts with **"BatchJobNotification"**. This sample project demonstrates how to submit an AWS Batch job. In its initial state the job is asynchronous. The state machine submits the job to the AWS Batch service but does not wait for the job to complete. Instead it immediately moves onto the next state and sends a Notify Success message to an Amazon SNS topic.

Here is what the initial workflow looks like:

![Module 3 Workflow](/static/img/module-3/initial-workflow.png)

Here is what the Task definition looks like for the Batch job. Take note of the Resource node.

![Module 3 Code](/static/img/module-3/initial-code.png)

Now go ahead and "Start execution" on this state machine. You may use the default input. The Batch service is now performing a task, which may take minute or more to finish. But notice how quickly this workflow completes.

Now imagine that we need our state machine to stay synchronized with the job in order to report on failures as soon as possible.
