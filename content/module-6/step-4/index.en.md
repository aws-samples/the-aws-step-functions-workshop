---
title: 'Execute the state machine and review results'
weight: 84
---

1. Click the `InputOutputProcessingMachine` state machine from the Step Functions console.
2. Click on **Start execution** and use the JSON below as your input payload.
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
3. Once the execution is successful, review the output in the `Execution output` tab. Notice how the data block in the input json is added to the output of the lambda function. This output would be passed to the next state in your workflow.

4. Click on the **Data flow simulator** button in the Graph Inspector. This tool simulates the order of data processing that occurs in a single Task state during execution.

  ![Data flow simulator](/static/img/module-6/simulator.png)

::alert[**Congratulations!** You have executed a state machine using the using the Input and Output data processing features.]{type="success"}