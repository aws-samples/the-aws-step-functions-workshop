---
title: 'Execute the state machine and review results'
weight: 75
---

1. In the [Step Functions](https://console.aws.amazon.com/states/home) console, navigate to **MapStateMachine** and click **Start execution**. You'll need to replace the default execution payload. Expand the `Execution Payload` below, then copy/paste the JSON as your execution payload.
   ::::expand{header="Execution Payload (Click to expand)" defaultExpanded=false}
   :::code{showCopyAction=true showLineNumbers=false language=json}
   {
      "Data": [
         {
         "orderId": "1",
         "customerId": "1",
         "priority": "HIGH"
         },
         {
         "orderId": "2",
         "customerId": "2",
         "priority": "HIGH"
         },
         {
         "orderId": "3",
         "customerId": "3",
         "priority": "HIGH"
         },
         {
         "orderId": "4",
         "customerId": "4",
         "priority": "LOW"
         },
         {
         "orderId": "5",
         "customerId": "5",
         "priority": "HIGH"
         },
         {
         "orderId": "6",
         "customerId": "6",
         "priority": "LOW"
         },
         {
         "orderId": "7",
         "customerId": "7",
         "priority": "HIGH"
         }
      ]
   }
   :::
   ::::

2. The execution should finish within a few seconds. When the execution is complete, go through the Map state iterations in the **Table View**.
   1. Click on the grey + symbol to expand Map State iterations.
   2. Expanding Map State Iterations #0 to #2, #4, and #6 shows that the State Machine followed the path for `HIGH` priority items, inserting the order details for those items in the input array into DynamoDB.
   3. Expanding the Map State Iterations for #3 and #5 shows that the State Machine followed the path for `LOW` priority items, which is a Success state, detecting that the item was a `LOW` priority item.
   4. The default max concurrency for Map state is 1 iteration at a time, which means we're processing the array in sequential fashion. Right after the first map state iteration finishes, the second one begins, and so on. You can see the details of iteration durations and timestamps in the Duration, Timeline, and Started After columns. In this execution, you'll see how each iteration of the Map state began after the previous one ended. In the next step, we'll demonstrate how to update your state machine to run multiple iterations in parallel. 
   5. You may also check [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) table to see if items have been successfully put into the **MapStateTable**.

![Table View with 1 Branch](/static/img/module-5/table-view-1-branch.png)

3. Update the State Machine to increase the Maximum concurrency value for the Map state.
   1. Click on the Map state in the Workflow Studio canvas.
   2. Scroll down within the Configuration tab until you see the Maximum concurrency setting.
   3. Update the value to 2 parallel iterations.
   4. This means our Map state will process up to 2 items from the input array in parallel. Increasing the number of parallel iterations allows us to process bigger sets of data in a shorter amount of time vs processing each item sequentially.
   5. Save your changes to the state machine using the `Apply and exit` button.

4. Start a new execution of the state machine with the same execution payload from Step 2.

   ::::expand{header="Execution Payload (Click to expand)" defaultExpanded=false}
   :::code{showCopyAction=true showLineNumbers=false language=json}
   {
      "Data": [
         {
         "orderId": "1",
         "customerId": "1",
         "priority": "HIGH"
         },
         {
         "orderId": "2",
         "customerId": "2",
         "priority": "HIGH"
         },
         {
         "orderId": "3",
         "customerId": "3",
         "priority": "HIGH"
         },
         {
         "orderId": "4",
         "customerId": "4",
         "priority": "LOW"
         },
         {
         "orderId": "5",
         "customerId": "5",
         "priority": "HIGH"
         },
         {
         "orderId": "6",
         "customerId": "6",
         "priority": "LOW"
         },
         {
         "orderId": "7",
         "customerId": "7",
         "priority": "HIGH"
         }
      ]
   }
   :::
   ::::

5. The execution should finish within a few seconds. When the execution is complete, go through the Map state iterations in the **Table View**.
   1. The iterations will have the same processing results for `HIGH` vs `LOW` items.
   2. We can see our parallel iterations in action by viewing the Timeline and Started After columns.
   3. Iteration #0 and Iteration #1 started at the same time.
   4. When Iteration #0 finished, Iteration #2 began. The Map state creates new workflow branches as each previous workflow branch is complete, without waiting for all the current workflow branches to finish. Even though Iteration #1 isn't done, the Map state started on Iteration #2.
   5. When Iteration #1 finished, Iteration #3 began.
   6. Iteration #3 did not result in inserting an item into DynamoDB, so the duration was very short.
   7. When Iteration #3 finished, Iteration #4 began.

In terms of total processing time, this execution took roughly half as long as the execution with only 1 parallel iteration. This is because Step Functions wasn't restricted to processing 1 item at a time and wait for each iteration with `HIGH` priority items to finish writing to DynamoDB before getting started on the next item.

![Table View with 2 Parallel Branches](/static/img/module-5/table-view-2-parallel.png)

::alert[**Congratulations!** You learned about how to use Map and Choice states in a state machine!]{type="success"}

::alert[**Congratulations!** You also took advantage of Map state concurrency settings to increase your data processing speed.]{type="success"}