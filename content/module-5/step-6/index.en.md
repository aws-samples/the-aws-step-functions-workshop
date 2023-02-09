---
title: 'Increase Map state concurrency and run workflow again'
weight: 76
---
1. Click on **Edit State Machine** in the top right corner.
![EDIT](/static/img/module-5/edit-state-machine.png)

2. Open the **MapStateStateMachine** in Workflow Studio by clicking Workflow Studio button on the right side of the screen.
![EDIT](/static/img/module-5/workflow-studio-button.png)

If you see the following screen, you're in the right place.

![EDIT](/static/img/module-5/module5-workflowstudio.png)

3. Update the State Machine to increase the Maximum concurrency value for the Map state. Expand the screenshot below to see how to update the setting, or follow the instructions below.
   1. Click on the Map state in the Workflow Studio canvas.
   2. Scroll down within the Configuration tab until you see the Maximum concurrency setting.
   3. Update the value to 2 parallel iterations.
   4. This means our Map state will process up to 2 items from the input array in parallel. Increasing the number of parallel iterations allows us to process larger datasets in a shorter amount of time vs processing each item sequentially.
   5. Save your changes to the state machine using the `Apply and exit` button.

::::expand{header="Map State Configuration Panel (Click to expand)" defaultExpanded=false}
![EDIT](/static/img/module-5/map-state-configuration-parallel.png)
::::

1. Start a new execution of the state machine with the same payload from the previous execution.

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
   1. The iterations will have the same processing results for `HIGH` vs `LOW` items.
   2. We can see our parallel iterations in action by viewing the Timeline and Started After columns.
   3. Iteration #0 and Iteration #1 started at the same time.
   4. When Iteration #0 finished, Iteration #2 began. The Map state creates new workflow branches as each previous workflow branch is complete, without waiting for all the current workflow branches to finish. Even though Iteration #1 isn't done, the Map state started on Iteration #2.
   5. When Iteration #1 finished, Iteration #3 began.
   6. Iteration #3 did not result in inserting an item into DynamoDB, so the duration was very short.
   7. When Iteration #3 finished, Iteration #4 began.

In terms of total processing time, this execution took roughly half as long as the execution with only 1 parallel iteration. This is because Step Functions wasn't restricted to processing 1 item at a time and wait for each iteration with `HIGH` priority items to finish writing to DynamoDB before getting started on the next item.

![Table View with 2 Parallel Branches](/static/img/module-5/table-view-2-parallel.png)

::alert[**Congratulations!** You also took advantage of Map state concurrency settings to increase your data processing speed.]{type="success"}