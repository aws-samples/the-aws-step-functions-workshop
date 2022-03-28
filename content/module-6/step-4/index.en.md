---
title: 'Execute the state machine and review results'
weight: 83
---

1. Click on the state machine `Lambda-input-output-processing-sm` or whatever name you provided in the previous step where you created the state machine.
2. Click on **Start execution** and use the below as your input payload.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "An input comment.",
   "data": {
      "val1": 23,
      "val2": 17
   },
   "extra": "foo",
   "lambda": {
      "who": "AWS Step Functions"
   }
}
:::
3. Once the execution is successful, review the output in the `Execution output` tab. See how the data block in the input json gets added to the output of the lambda function. This output would be passed to the next state in your workflow.
