---
title: 'Module 3 - Run a Job (.sync)'
weight: 50
---

For integrated services such as AWS Batch and Amazon ECS, Step Functions can wait for a task to complete before progressing to the next state. This task orchestration pattern is called [Run a Job (.sync)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-sync) in the documentation. To see a list of the integrated services that support synchronization, see [Optimized integrations for Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).

To see a sample High Performance Computing (HPC) project using AWS Batch, Step Functions and Run a Job (.sync) view [this blog post](https://aws.amazon.com/blogs/compute/orchestrating-high-performance-computing-with-aws-step-functions-and-aws-batch/).

In this module you will configure and run a synchronized task using **Run a Job (.sync)**.