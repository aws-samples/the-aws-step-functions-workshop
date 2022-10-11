---
title: 'Module 6 - Input and Output Processing'
weight: 80
---
A Step Functions execution receives JSON text as input and passes that input to the first state in the workflow. Each individual state receive JSON as input and usually passes JSON as output to the next state. Understanding how this information flows from state to state and learning how to filter and manipulate this data is critical to designing and implementing effective workflows in Step Functions.

In the Amazon States Language, these fields filter and control the flow of JSON from state to state:

- `InputPath`
- `OutputPath`
- `ResultPath`
- `Parameters`
- `ResultSelector`

Read the documentation to learn more about [Input and Output Processing](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-input-output-filtering.html).

**Estimated Duration: 25 minutes**