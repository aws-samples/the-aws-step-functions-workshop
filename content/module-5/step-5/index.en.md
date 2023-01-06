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

::alert[**Congratulations!** You learned about how to use Map and Choice states in a state machine!]{type="success"}