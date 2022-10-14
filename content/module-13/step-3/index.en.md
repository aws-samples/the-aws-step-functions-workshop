---
title: 'Overview of the State Machine'
weight: 143

---

In your account, you have a state machine with a name beginning with _ParentStateMachine_. The state machine currently is currently a Standard workflow. As mentioned in the beginning of the module, this might be necessary if your workflow utilizes a feature only available to Standard workflows, like the .waitForTaskToken feature, or because the workflow duration could exceed 5 minutes, or because you need an "exactly once" execution model.  

However, note the circled steps below. Let’s assume that these steps are idempotent and would be fine in an "at least once" execution model, like the one Express workflows provide. We could move those steps to a nested Express workflow.  

![Steps that could move to an Express workflow](/static/img/module-13/state-machine-express-step-candidates.png)
