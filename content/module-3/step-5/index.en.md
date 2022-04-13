---
title: 'Execute synchronous task'
weight: 55
---

Now run the state machine again using the default input. This time you will notice that the `Submit Batch Job` state will not advance until the job is completed.

![Module 3 Workflow](/static/img/module-3/modified-workflow.png)

Once the job completes (usually ~1-2 mins) the state machine will proceed.

::alert[**Congratulations!** You have executed a state machine using a synchronous task pattern.]{type="success"}