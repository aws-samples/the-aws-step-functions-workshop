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

Where metrics help you keep track of what is happening within your system, *logs* help you keep track of what already happened within your application or system. Logs are time-stamped records of events that include failures, errors, state transformations, or even who accessed your system at a certain time. Logs can be in an unstructured, semi-structured or structure format.

A *trace* is a representation of a series of causally related distributed events that encode the end-to-end request flow through a distributed system.

Logging, monitoring, and tracing are all important for maintaining the reliability, availability, and performance of your applications. There are several tools available to use with Step Functions that help with each of the three pillars of observability. 

Review the documentation:
- [Logging and monitoring in AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/monitoring-logging.html)
- [Tracking execution status using Amazon EventBridge](https://docs.aws.amazon.com/step-functions/latest/dg/cw-events.html)
- [X-Ray and Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html)


