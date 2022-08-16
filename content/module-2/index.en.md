---
title: 'Module 2 - Request Response'
weight: 40
---

When Step Functions calls another service using the `Task` state, the default pattern is [Request Response](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-default). With this task orchestration pattern, Step Functions will call the service and then immediately proceed to the next state. The `Task` state will not wait for the underlying job to complete.

In this module you will run a `Task` using the Request Response pattern.

**Estimated Duration: 15 minutes**