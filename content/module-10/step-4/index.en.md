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

::alert[**Congratulations!** You have successfully completed the module.]{type="success"}
