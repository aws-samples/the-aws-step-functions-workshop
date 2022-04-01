---
title: 'Execute the state machine'
weight: 104
---

**Start a New Execution**

1. Click on **BatchJobNotificationStateMachine** and then choose **Start Execution**.

**(Optional)** To identify your execution, you can specify a name for it in the Name box. By default, Step Functions generates a unique execution name automatically.

**Note**

Step Functions allows you to create state machine, execution, and activity names that contain non-ASCII characters. These non-ASCII names don't work with Amazon CloudWatch. To ensure that you can track CloudWatch metrics, choose a name that uses only ASCII characters.

Optionally, you can go to the newly created state machine on the Step Functions Dashboard, and then choose New execution.

When an execution is complete, you can select states on the Visual workflow and browse the Input and Output under Step details.

 ---
**Error Handling - Failure Scenario**

Let's see how AWS Step Functions will implement error handling when any error is returned from AWS Batch service. As you can see in the screenshots below, after step functions has received an error it did the following:

>1. Retried the batch job two more times as MaxAttempts is set to 2, so you will see total 3 executions.
>2. It will wait for the duration of IntervalSeconds - 30s between the retries with BackoffRate of - 2.5 which is the multiplier by which the retry interval increases during each attempt.
>3. After retries, it will execute the 'Notify Failure' task and send a notification to the SNS topic.


![Flowchart](/static/img/module-10/errorhandlingbatchjob3.png)
![Flowchart](/static/img/module-10/errorhandlingbatchjob4.png)
![Flowchart](/static/img/module-10/errorhandlingbatchjob2.png)

::alert[**Congratulations!** You have successfully completed the module.]{type="success"}
