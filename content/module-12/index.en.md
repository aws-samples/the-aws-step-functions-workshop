---
title: 'Module 12 - Observability'
weight: 140
---
Observability helps you understand what is happening in your systems and applications. Gaining observability helps you detect, investigate, and remediate problems.

The three pillars of observability are:
  - Metrics
  - Logs
  - Traces

*Metrics* are a numeric representation of data measured over intervals of time. Metrics provide data about the performance of your systems. You can think of a metric as a single variable used to monitor an aspect of your system. When you combine all these individual metrics, you are able to see how your application is performing over time.

*Logs* help you keep track of events that have occurred within your application or system. Logs are time-stamped records can include events like failures, errors, state transformations, or even who accessed your system at a certain time. Logs can be recorded in unstructured, semi-structured or structured formats.

*Traces* are representations of a series of causally related distributed events. Traces may encode end-to-end request flows through a distributed system.

Monitoring metrics, logs, and traces can help you understand the availability, performance and health of your applications. AWS provides several tools you can use with Step Functions to monitor these three pillars of observability. 

Review the documentation:
- [Logging and monitoring in AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/monitoring-logging.html)
- [Tracking execution status using Amazon EventBridge](https://docs.aws.amazon.com/step-functions/latest/dg/cw-events.html)
- [AWS X-Ray and Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html)

**Estimated Duration: 30 minutes**
