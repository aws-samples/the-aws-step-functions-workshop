---
title: 'Module 5 - Choice State and Map State'
weight: 70
---

## Choice state

A [Choice state](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) adds branching logic to a state machine. In addition to most of the common state fields, `Choice` states contain the following additional fields:

- Choices (Required) - an array of Choice Rules that determines which state the state machine transitions to next.

- Default (Optional, Recommended) - the name of the state to transition to if none of the transitions in Choices is taken.

## Map state

The [Map state](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) can run a set of parallel steps for each element of an input array. To configure a `Map` state, you define an `Iterator`, which is a complete child workflow execution. When a Step Functions execution enters a `Map` state, it will iterate over a JSON array in the state input. For each item, the `Map` state will execute one child workflow execution, potentially in parallel. When all child workflow execution executions complete, the `Map` state will return an array containing the output for each item processed by the Iterator.

**Estimated Duration: 20 minutes**
