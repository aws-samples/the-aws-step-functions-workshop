---
title: 'Overview of the concept'
weight: 122
---

This module demonstrates **error handling** using `Catch` and `Retry` fields. `Task` and `Parallel` states can have a field named `Retry`, whose value must be an array of objects known as retriers. An individual retrier represents a certain number of retries, usually at increasing time intervals. `Task`, `Map` and `Parallel` states can have a field named `Catch`. This field's value must be an array of objects, known as catchers. 

When a state has both Retry and Catch fields, Step Functions uses any appropriate retriers first, and only afterward applies the matching catcher transition if the retry policy fails to resolve the error.

This module uses a Lambda function to show how Step Functions handles `Catch` and `Retry`.

Review the documentation:
- [Error handling in Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html)
- [Error handling in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html)


