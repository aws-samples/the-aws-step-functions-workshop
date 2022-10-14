---
title: 'Module 13 - Nested Workflows'
weight: 140
---
Nested workflows are useful when you want to package parts of a state machine together, for example to be reused as a building block across multiple workflows. But nested workflows also allow you to mix Standard and Express workflows. Express workflows are often less costly than the equivalent Standard workflow, but it’s important to understand the differences between them. Your workflow might contain some steps that require functionality not available with Express workflows, such as the .waitForTaskToken and .sync invoke methods, or your workflow may run for more than 5 minutes. Or, you might require an “exactly once” workflow execution model. In this case, those steps would be part of a Standard workflow.  

However, some steps might be idempotent, meaning that they be executed more than once without affecting the end result. Those steps would work well in an Express workflow, with its “at least once” delivery model. Those steps could be pulled out of your Standard workflow and placed in a nested Express workflow. Doing so could improve performance and reduce cost. This module will show you how to do that.

Review the documentation:

- [Standard vs. Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)

**Estimated Duration: 20 minutes**
