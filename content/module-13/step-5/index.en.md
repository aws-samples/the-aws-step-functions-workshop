---
title: 'Review the Cost Impact'
weight: 155

---

Cost and performance are key reasons to consider nesting Express workflows within Standard workflows.  

## Pricing

|**Standard Workflows**|**Express Workflows**|
---|---|
|Standard Workflows are charged based on the number of state transitions required to run a workload. Step Functions counts a state transition each time a step of your workflow runs. You are charged for the total number of state transitions across all your Standard state machines, including retries.|Express Workflows are charged based on the number of times your state machine executes and the duration. Duration is calculated from the time that your workflow begins running until it completes or otherwise finishes, rounded up to the nearest 100 ms, and the amount of memory used in running your workflow, billed in 64-MB chunks.|

## Pricing Comparison

Moving the 4 Lambda task steps from our Standard Workflow and replacing them with one call to a nested Express Workflow eliminates 3 steps from each state machine execution.

Let’s say you ran the original Standard Workflow 1,000 times in the N. Virginia region. You would be charged for 3,000 more state transitions than the modified workflow.

### Original Workflow

**Total cost** = `(number of transitions per execution x number of executions) x $0.000025`  
**Total cost** = `(3 X 1000) X 0.000025 = $0.075`  
(*Note: this does not include the 4,000 state transitions included in the AWS Free Tier every month*)  

### Nested Express Workflow

Instead, we’re now charged for the Express Workflow. Let us assume that each Express Workflow invocation runs for an average of 11,300ms and does not use more than 64-MB of memory.  

**Duration cost** = `(Avg billed duration ms / 100) * price per 100 ms`  
**Execution cost** = `$0.000001 per request`  
**Total cost** = `(Execution cost + Duration cost) x Number of Requests`  

**Duration cost** = `(11300 MS /100) * $ 0.0000001042 = $0.0000117746`  
**Execution cost** = `$0.000001 per request`  
**Total cost** = `($0.000001 + $0.0000117746) x 1000 = $0.01`  

To summarize, in this example, it costs 7.5x more to keep those steps in the Standard Workflow. Moving the steps that do not require the execution guarantees of a Standard Workflow into a nested Express Workflow can result in savings for your workload.

### How Express Workflow Duration Affects Cost

The cost savings is dependent on the number of steps you remove from your Standard Workflow and the duration of the nested Express Workflow. In the example, you removed three (3) state transitions by replacing four (4) task steps with one nested workflow step. The chart below shows the cost of 1,000 executions of the Standard workflow steps, plotted against the cost of the same steps when moved to a nested Express workflow, over a variety of durations. As you can see, the Express workflow is less expensive, even if it runs for one minute.

![Cost comparison chart](/static/img/module-13/cost-comparison-by-duration.png)
