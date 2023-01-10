---
title: 'Use intrinsic functions to augment data processing'
weight: 86
---

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
