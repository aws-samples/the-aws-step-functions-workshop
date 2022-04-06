---
title: 'Review workflow'
weight: 32
---

Navigate to the Step Functions service and find the state machine that starts with **"TimerStateMachine"**. In this sample app we will execute a task after waiting for a specified delay. Click Edit to find the button for Workflow Studio:

![Workflow Studio Button](/static/img/module-1/workflow-studio.png)

Review the definition in Workflow Studio:

![Module 1 Workflow](/static/img/module-1/workflow.png)

The state machine is defined using Amazon States Language (ASL). Click the Definition button to view the ASL code. You can see that the ASL contains a "Wait" state.

![Module 1 Code](/static/img/module-1/code.png)
