---
title: 'Overview of the architecture'
weight: 73
---

This module demonstrates dynamic parallelism using the Map and Choice states. It contains the following resources:

- One Amazon DynamoDB table

- One AWS Step Functions state machine

In this module, you'll pass in a JSON array of orders to be processed by your state machine. A Map state is used to iterate over the input array, similar to a loop in programming languages. In each iteration, the map state dynamically creates separate workflow branches. A choice state is used to determine what action to take for that item in the JSON array, similar to an if statement in programming languages. If the current item's `priority` field has a value `"HIGH"`, Step Functions writes the order details into DynamoDB. If the current item's `priority` field is `"LOW"`, no action is taken. 

![Visual Workflow](/static/img/module-5/visual-workflow.png)

Learn more about [Step Functions service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
