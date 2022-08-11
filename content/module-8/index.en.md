---
title: 'Module 8 - Error Handling'
weight: 100
---
Any state can encounter runtime errors. Errors can happen for various reasons:

- State machine definition issues (for example, no matching rule in a Choice state)

- Task failures (for example, an exception in a Lambda function)

- Transient issues (for example, network partition events)

By default, when a state reports an error, Step Functions causes the execution to fail entirely. However, Step Functions has error handling features that enable you to retry or catch states that fail. Error handling features can define retry protocols and also catch and handle a variety of error conditions.

This module demonstrates **error handling** by using Lambda functions to simulate errors that are handled using the `Retry` and `Catch` fields. 

Review the documentation:
- [Error handling in Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html)
- [Error handling in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html)

Estimated Duration: 20 minutes