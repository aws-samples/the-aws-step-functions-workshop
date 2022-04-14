---
title: 'Build a state machine with a Parallel State and Integrate it with API Gateway'
weight: 94
---

### Create the State Machine

Follow the steps below to create a state machine using Workflow Studio.

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in your AWS console. Make sure you are in the correct region.
2. Click **Create state machine**.
3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Express** and click on `Next`.
   ![Studio Selection](/static/img/module-7/studio-selection.png)
4. You should see Workflow Studio.
   ![Studio Designer](/static/img/module-7/studio-designer.png)
5. Enter a `Comment` on the right side: 

```bash
A step functions workflow that executes tasks in parallel.
```

6. Drag and drop `Parallel` from the **Flow** section on the left side to the designer form where it says `Drag first state here`.
   ![Add Parallel State](/static/img/module-7/add-parallel-state.png)
7. You should have the three Lambda functions for this module deployed to your account. Add an action to invoke the first Lambda function.

- Drag & drop `AWS Lambda Invoke` from the **Actions** section on the left side to the designer form where it says `Drag state here`.
  ![Invoke Lambda Function 1](/static/img/module-7/lambda-invoke-function1.png)
- On the `Configuration` tab of the designer, enter `SumValues` for state name.
- In the API parameters section, select from the drop down of **Function name** the function with `SumFunction` in the name.
  ![Configuration Sum State](/static/img/module-7/configuration-sum-state.png)
- On the `Output` tab, uncheck the option for `Filter output with OutputPath` and check the option for `Transform result with ResultSelector`. Paste the following json in the textbox:

  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "sum.$": "$.Payload.sum" }
  :::
  ![Output Sum State](/static/img/module-7/output-sum-state.png)

8. Add an action to invoke the second Lambda function.

- Drag & drop `AWS Lambda Invoke` from the **Actions** section on the left side to the designer form where it says `Drag state here`.
  ![Invoke Lambda Function 2](/static/img/module-7/lambda-invoke-function2.png)
- On the `Configuration` tab of the designer, enter `AverageValues` for state name.
- In the API parameters section, select from the drop down of **Function name** the function with `AvgFunction` in the name.
  ![Configuration Avg State](/static/img/module-7/configuration-avg-state.png)
- On the `Output` tab, uncheck the option for `Filter output with OutputPath` and check the option for `Transform result with ResultSelector` then paste the following json in the textbox
  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "avg.$": "$.Payload.avg" }
  :::
  ![Output Avg State](/static/img/module-7/output-avg-state.png)

9. Add an action to invoke the third Lambda function.

- Drag & drop `AWS Lambda Invoke` from the **Actions** section on the left side to the designer form between the two existing actions.
  ![Invoke Lambda Function 3](/static/img/module-7/lambda-invoke-function3.png)
- On the `Configuration` tab of the designer, enter `MaxMinValues` for state name.
- In the API parameters section, select from the drop down of **Function name** the one with `MaxMinFunction` in the name.
  ![Max Min State](/static/img/module-7/configuration-maxmin-state.png)
- On the `Output` tab, uncheck the option for `Filter output with OutputPath` and check the option for `Transform result with ResultSelector` then paste the following json in the textbox
:::code{showCopyAction=true language=json}
{
"max.$": "$.Payload.max",
"min.$": "$.Payload.min"
}
:::
  ![Output Max Min State](/static/img/module-7/output-maxmin-state.png)

10. Click on **Next** and review the generated code and click **Next** again.

- Provide a name to this state machine: `ParallelProcessingMachine`. Choose an existing IAM role with the name containing `StepFunctionsIamRole`.
- Leave the rest of the defaults and click on **Create state machine**.
  You now have a state machine that can run parallel calculations. Copy the ARN of the State Machine and save it. You will need it to create the integration with API Gateway.

### Setting up the integration between API Gateway and Step Functions

1. Go to the [API Gateway console](https://console.aws.amazon.com/apigateway/home) and select the API created for this module: `API Gateway State Machine integration`.
   ![API Console](/static/img/module-7/api-console.png)
2. From the list of resources find the execution resource and click on `POST`
   ![API Execution](/static/img/module-7/api-execution.png)
3. Click on `Integration Request`
4. For the `Integration type` select `AWS Service`
5. Configure the integration:

- **AWS Region**: select the AWS region where you created the State Machine
- **AWS Service**: select `Step Functions` from the dropdown
- **HTTP Method**: select `POST`
- **Action Type**: select `Use action name`
- **Action**: type `StartExecution`
- **Execution role**: find in [IAM](https://console.aws.amazon.com/iamv2/home) the role with `IntegrationIamRole` in its name and use the ARN of this role
  ![API Integration Setup](/static/img/module-7/api-integration-setup.png)
- Click `Save`. When prompted if you are sure that you want to switch the integration click `Ok`.
  You have now set up an integration between API Gateway and Step Functions.
