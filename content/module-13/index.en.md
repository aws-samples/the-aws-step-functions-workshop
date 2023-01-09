---
title: 'Module 13 - Nested Express Workflows'
weight: 150
---
As you gain more experience with Step Functions, and the complexity of your state machines increases, you may start looking for ways to reduce the cost of your state machine executions. For Standard workflows, you pay per state transition, and large, complex workflows can become expensive at scale. One way to reduce cost is to determine if any steps could be moved to an Express workflow.  Unlike Standard workflows, Express workflows are charged for how long they run, regardless of the number of state transitions, as well as a per execution cost.

Express workflows differ from Standard workflows in a few important ways:

1. Standard workflows have an "exactly once" execution model, whereas Express workflows are "at least once."
1. Express workflows do not support certain invocation methods, like `sync` and `waitForTaskToken`.
1. Express workflows have a maximum duration of 5 minutes, whereas Standard workflows can run for up to 365 days.

For a full comparison of Standard and Express workflows, please refer to the [documentation](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html).

As you examine your workflows, you might identify steps that could be moved into an Express workflow, perhaps because they are [idempotent](https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-idempotent/), meaning that they can be executed more than once without affecting the end result. In such a case, you could create an Express workflow containing those steps and then execute that nested workflow from within your existing Standard workflow, realizing cost savings by doing so. This module will guide you through the process of doing that.

Review the documentation:

- [Standard vs. Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Cost-optimization using Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/cost-opt-exp-workflows.html)
- [Building cost-effective AWS Step Functions workflows](https://aws.amazon.com/blogs/compute/building-cost-effective-aws-step-functions-workflows/)
- [Selective Checkpointing Example](https://docs.aws.amazon.com/step-functions/latest/dg/sample-project-express-selective-checkpointing.html)

**Estimated Duration: 20 minutes**
