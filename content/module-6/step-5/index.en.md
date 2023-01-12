---
title: 'Use the Data Flow Simulator and intrinsic functions for data processing'
weight: 85
---

1. Click on the **Data flow simulator** button in the Graph Inspector.

The Data Flow Simulator allows developers to simulate the order of data processing that occurs in a single Task state during execution. This helps developers understand how to filter and manipulate data as it flows from state to state. Developers can specify a starting JSON input and evaluate it through each of the processing path stages.

The simulator starts at the State Input stage. The input field automatically validates the JSON object, and highlights any syntax errors.

![Data flow simulator](/static/img/module-6/simulator.png)

2. Use the Data flow simulator to test data processing for the `InputOutputProcessingMachine` input payload. Replace the default State Input with the input payload below and choose the InputPath stage. Set the InputPath to $.lambda.

:::code{showCopyAction=true showLineNumbers=false language=json}
{
"comment": "An input comment.",
"data": {
"value1": 23,
"value2": 17
},
"extra": "foo",
"lambda": {
"who": "AWS Step Functions"
}
}
:::

![Data flow simulator](/static/img/module-6/input-path.png)

The left panel shows the state input before the InputPath is applied. The panel on the right shows the state input after InputPath is applied.

Developers can use the Data Flow Simulator to quickly implement the data processing they need in their state machines.
Feel free to keep testing values for Parameters, ResultSelector and OutputPath within the Data Flow Simulator. Please note that you will need to replace the default values throughout the simulator based on your payload transformations.

For more information on the Data Flow Simulator, see the [AWS Blog](https://aws.amazon.com/blogs/compute/modeling-workflow-input-output-path-processing-with-data-flow-simulator/).

::alert[**Congratulations!** You used the Data Flow Simulator to practice Input and Output data processing with Amazon States Language!]{type="success"}

# Using Intrinsic Functions to augment your data processing

The Amazon States Language (ASL) provides several intrinsic functions, also known as intrinsics, that help you perform basic data processing operations without using a Task state.
Examples of basic operations include math operations, creating unique ID's or merging JSON objects. You can use intrinsics like `States.MathAdd`, `States.UUID`, or `States.JsonMerge` in your workflow to avoid the overhead of a Lambda function to perform those operations.

For a full list of intrinsics, see the documentation page [here](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-intrinsic-functions.html).

In this section, you'll use the `States.MathAdd` intrinsic to add two numbers together without needing to use a Lambda function to perform the operation.
1. Navigate back to Workflow Studio for the `InputOutputProcessingMachine` state machine.
2. Add a new Pass State to the state machine after the Lambda Invoke state. Note that you aren't limited to Pass States for intrinsics, you'll be able to use them in any state that supports Parameters.

![Pass State Input](/static/img/module-6/pass-state-diagram.png)

3. In the Input tab of the Pass state, fill out the following value in the parameter text field. Note that you'll need to add the `.$` suffix when using intrinsics.
    ```json
      {
        "Sum.$": "States.MathAdd($.value1, $.value2)"
      }
    ```

![Pass State Input](/static/img/module-6/pass-state-input-intrinsic.png)

4. Click on **Start execution** and use the JSON below as your input payload.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "An input comment.",
   "data": {
      "value1": 23,
      "value2": 17
   },
   "extra": "foo",
   "lambda": {
      "who": "AWS Step Functions"
   }
}
:::
5. Once the execution is successful, review the output in the `Execution output` tab. You'll see the sum field has the sum of value1 and value2 from the input.

![Execution Output](/static/img/module-6/intrinsic-execution-output.png)

::alert[**Congratulations!** You used an intrinsic function to perform basic data processing without needing to write any code!]{type="success"}