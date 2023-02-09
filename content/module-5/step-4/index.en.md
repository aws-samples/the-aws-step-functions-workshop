---
title: 'Locate your resources and configure your state machine'
weight: 74
---

### Locate your resources

Navigate to the services below in the AWS console to familiarize yourself with the resources. Make sure you are in the correct region. Copy the SNS Topic ARN (Amazon Resource Name) to a notepad. You will need this value later in the module.

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) - find **MapStateTable**

### View your state machine

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in the AWS console.

2. Locate the state machine that contains **MapStateStateMachine** in its name. Click on it and then click on **Edit** in the top right corner.

![EDIT](/static/img/module-5/map-state-definition-edit.png)

3. Open the **MapStateStateMachine** in Workflow Studio by clicking Workflow Studio button on the right side of the screen.
![EDIT](/static/img/module-5/workflow-studio-button.png)

![EDIT](/static/img/module-5/module5-workflowstudio.png)

4. Click on the Map state `Iteration Over Input Array` and note the configuration details.
   1.  **Processing mode: Inline** - This is the mode for processing relatively smaller inputs and data sources. If you'd like to learn more about how to process larger datasets such as those in S3, check out the Distributed Map module later on in the workshop!
   2.  **Item Source - Provide a path to the items array** - This setting is used to point the Map state to the specific array within the JSON input.
   3.  **Maximum concurrency** - This setting is used to define how many items we want to process in parallel. The default is 0, which means we'll process the data sequentially, one item at a time. We'll explore this setting in the module.
   ::::expand{header="Map State Configuration Screenshot (Click to expand)" defaultExpanded=false}
  ![Map State Configuration](/static/img/module-5/map-state-configuration.png)
  ::::
1. Select the Choice state `Priority Filter` and view the Choice Rules we've defined in the state machine.
   1. **Rule #1**: $.priority == `LOW`. Within each item of the array, we'll check the priority value, and Step Functions will route the item to the defined state for that path. In this case, `LOW` priority items are routed to a success state `Low Priority Order Detected`, they are not written to the DynamoDB table.
   2. **Rule #2**: $.priority == `HIGH`. In this case, `HIGH` priority items go to `Insert High Priority Order` and are written to the DynamoDB table.
   3. When working with Choice states in your own state machines, use Workshop Studio and `Add new choice rule` button to quickly build the logic you need to route your data. 
  ::::expand{header="Choice State Configuration Screenshot (Click to expand)" defaultExpanded=false}
  ![Choice State Configuration](/static/img/module-5/choice-state-configuration.png)
  ::::