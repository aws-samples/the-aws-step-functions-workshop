---
title: 'Execute initial workflow'
weight: 61
---

Navigate to the state function in your account that begins with **"WaitForCallbackStateMachine"**. This state machine sends a task to SQS but the callback for it is not yet implemented.

Execute the state machine with default input and you'll notice that this execution will become paused indefinitely at the `Start Task and Wait For Callback` state.

![Module 4 Workflow](/static/module4-initial-workflow.png)
