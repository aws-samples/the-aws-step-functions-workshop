---
title: 'Use the Data Flow Simulator to test data processing'
weight: 85
---

## Using the Data Flow Simulator

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
