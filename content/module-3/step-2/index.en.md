---
title: 'Overview of the concept'
weight: 32
---

In this module we will implement a synchronized task orchestration pattern called [Run a Job (.sync)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-sync). With this pattern, Step Functions will call a service integration and wait until its job is complete before advancing to the next state. To see a list of the integrated services that support synchronization, see [Optimized integrations for Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).