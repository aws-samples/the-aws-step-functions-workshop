---
title: 'Module 13 - Nested Workflows'
weight: 150
---
As you gain more experience with Step Functions, and the complexity of your state machines increases, you may want to consider nested workflows to help build cost-effective and reusable workflows. Nested workflows also allow you to mix Standard and Express workflows. Express workflows are often less costly than the equivalent Standard workflow, but it’s important to understand the differences between them. Your workflow might contain some steps that require functionality not available with Express workflows, such as the .waitForTaskToken and .sync invoke methods, or your workflow may run for more than 5 minutes. Or, you might require an “exactly once” workflow execution model. In this case, those steps would be part of a Standard workflow.  

However, some steps might be [idempotent](https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-idempotent/), meaning that they can be executed more than once without affecting the end result. Those steps would work well in an Express workflow, with its “at least once” delivery model. Those steps could be pulled out of your Standard workflow and placed in a nested Express workflow. Doing so could improve performance and reduce cost. This module will show you how to do that.

Review the documentation:

- [Standard vs. Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Building cost-effective AWS Step Functions workflows](https://aws.amazon.com/blogs/compute/building-cost-effective-aws-step-functions-workflows/)
- [Selective Checkpointing Example](https://docs.aws.amazon.com/step-functions/latest/dg/sample-project-express-selective-checkpointing.html)

**Estimated Duration: 20 minutes**
