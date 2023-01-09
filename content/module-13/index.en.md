---
title: 'Module 13 - Nested Express Workflows'
weight: 150
---
As you gain more experience with Step Functions, and the complexity of your state machines increases, you may start looking for ways to simplify and optimize your state machine executions. Nesting workflows inside of other workflows is a powerful tool. From a modularity perspective, nested workflows allow you to create reusable state machines which can be executed by other workflows, promoting reuse. Nesting workflows of different types, like an Express workflow nested inside of a Standard workflow, can help you reduce cost. For Standard workflows, you pay per state transition, and large, complex workflows can become expensive at scale. One way to reduce cost is to determine if any steps could be moved to an Express workflow.  Unlike Standard workflows, Express workflows are charged for how long they run, regardless of the number of state transitions, as well as a per execution cost.

Express workflows differ from Standard workflows in a few important ways:

1. Standard workflows have an "exactly once" execution model, whereas Express workflows are "at least once."
1. Express workflows do not support certain invocation methods, like `sync` and `waitForTaskToken`.
1. Express workflows have a maximum duration of 5 minutes, whereas Standard workflows can run for up to 365 days.

For a full comparison of Standard and Express workflows, please refer to the [documentation](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html).

As you examine your workflows, you might identify steps that could be moved into an Express workflow, perhaps because they are [idempotent](https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-idempotent/), meaning that they can be executed more than once without affecting the end result. In such a case, you could create an Express workflow containing those steps and then execute that nested workflow from within your existing Standard workflow, realizing cost savings by doing so.

This module will guide you through the process using the AWS Console, but you can also develop nested workflows written in [Amazon States Language (ASL)](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) and deployed using [AWS CloudFormation](https://aws.amazon.com/cloudformation/) or the [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/), using the [AWS Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_stepfunctions_tasks.StepFunctionsStartExecution.html), or using third-party Infrastructure as Code (IaC) tools like Terraform and the Serverless Framework.

Review the documentation:

- [Standard vs. Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Cost-optimization using Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/cost-opt-exp-workflows.html)
- [Building cost-effective AWS Step Functions workflows](https://aws.amazon.com/blogs/compute/building-cost-effective-aws-step-functions-workflows/)
- [Selective Checkpointing Example](https://docs.aws.amazon.com/step-functions/latest/dg/sample-project-express-selective-checkpointing.html)

**Estimated Duration: 20 minutes**
