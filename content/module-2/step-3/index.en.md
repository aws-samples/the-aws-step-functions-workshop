---
title: 'Start execution'
weight: 43
---

Now go ahead and "Start execution" on this state machine using the following input values:

::code[{ "message": "Welcome to re:Invent!", "timer_seconds": 5 }]{showCopyAction=true language="js"}

Navigate to the event history for this execution. You will notice that the execution time for the Send SNS Message task is relatively fast. The state machine proceeds as soon as the SNS Publish API is called.

![Module 2 Result](/static/img/module-2/results.png)

In this case the `"Send SNS Task"` completed in 120ms. Review your own execution event history to compare results.
