---
title: 'Review the Cost Impact'
weight: 143

---

Cost and performance are key reasons to consider nesting Express workflows within Standard workflows.  

Standard Workflows are charged based on the number of state transitions required to run a workload. Step Functions counts a state transition each time a step of your workflow runs. You are charged for the total number of state transitions across all your Standard state machines, including retries.

On the other hand, Express Workflows are charged based on the number of requests and their duration. Duration is calculated from the time that your workflow begins running until it completes or otherwise finishes, rounded up to the nearest 100 ms, and the amount of memory used in running your workflow, billed in 64-MB chunks.

Removing the 4 separate steps from our Standard Workflow to invoke those Lambda functions and replacing it with one call to a nested Express Workflow eliminates 3 steps from each state machine execution.

Let’s say we ran the original Standard Workflow 1,000 times. We would be charged for 3,000 more state transitions than our modified workflow.  

**Total cost** = (number of transitions per execution x number of executions) x $0.000025
**Total cost** = (3 X 1000) X 0.000025 = $0.075 (*Note: this does not include the 4,000 state transitions included in the AWS Free Tier every month*)

Instead, we’re now charged for the Express Workflow. Let us assume that each Express Workflow invocation runs for an average of 11,300ms and does not use more than 64-MB of memory.  

**Duration cost** = (Avg billed duration ms / 100) * price per 100 ms
**Execution cost** = $0.000001 per request
**Total cost** = (Execution cost + Duration cost) x Number of Requests

**Duration cost** = (11300 MS /100) * $ 0.0000001042 = $0.0000117746
**Execution cost** = $0.000001 per request
**Total cost** = ($0.000001 + $0.0000117746) x 1000 = $0.01

In summary, in this scenario, it costs 7.5x more to keep those steps as a Standard Workflow, when the guarantees and additional functionality provided by Standard Workflows are not necessary.
