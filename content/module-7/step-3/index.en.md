---
title: 'Build a state machine with a Parallel State and Integrate it with API Gateway'
weight: 93
---

## Creating the State Machine

Three Lambda functions are already created for you in your AWS account. Follow the below steps to create a simple workflow using Workflow Studio.

1. Navigate to Step Functions in your AWS console. Make sure you are in the same AWS region that is assigned for this session.
2. If you are not on the `State machines` page, click on `State machines` on the left side menu and click **Create state machine**
3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Express** and click on `Next`.
   ![Studio Selection](/static/img/module-7/module-7-studio-selection.png)
4. You should see the designer studio now which will look like this.
   ![Studio Designer](/static/img/module-7/module-7-studio-designer.png)
5. For `Comment` on the right side, enter `A step functions example executing tasks in parallel`.
6. Drag & drop `Parallel` from the **Flow** section on the left side to the designer form where it says `Drag first state here`.
   ![Add Parallel State](/static/img/module-7/module-7-add-parallel-state.png)
7. Let's add the first action.

- Drag & drop `AWS Lambda` from the **Actions** section on the left side to the designer form where it says `Drag state here`.
  ![Invoke Lambda Function 1](/static/img/module-7/module-7-lambda-invoke-function1.png)
- On the `Configuration` tab of the designer, enter `SumValues` for state name.
- In the API parameters section, select from the drop down of **Function name** the one with `SumFunction` in the name.
  ![Configuration Sum State](/static/img/module-7/module-7-configuration-sum-state.png)
- On the `Output` tab, uncheck the option for `Filter output with OutputPath` and check the option for `Transform result with ResultSelector` then paste the following json in the textbox

  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "sum.$": "$.Payload.sum" }
  :::
  ![Output Sum State](/static/img/module-7/module-7-output-sum-state.png)

8. Let's add the second action.

- Drag & drop `AWS Lambda` from the **Actions** section on the left side to the designer form where it says `Drag state here`.
  ![Invoke Lambda Function 2](/static/img/module-7/module-7-lambda-invoke-function2.png)
- On the `Configuration` tab of the designer, enter `AverageValues` for state name.
- In the API parameters section, select from the drop down of **Function name** the one with `AvgFunction` in the name.
  ![Configuration Avg State](/static/img/module-7/module-7-configuration-avg-state.png)
- On the `Output` tab, uncheck the option for `Filter output with OutputPath` and check the option for `Transform result with ResultSelector` then paste the following json in the textbox
  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "avg.$": "$.Payload.avg" }
  :::
  ![Output Avg State](/static/img/module-7/module-7-output-avg-state.png)

9. Let's add the last action.

- Drag & drop `AWS Lambda` from the **Actions** section on the left side to the designer form between the two existing actions.
  ![Invoke Lambda Function 3](/static/img/module-7/module-7-lambda-invoke-function3.png)
- On the `Configuration` tab of the designer, enter `MaxMinValues` for state name.
- In the API parameters section, select from the drop down of **Function name** the one with `MaxMinFunction` in the name.
  ![Max Min State](/static/img/module-7/module-7-configuration-maxmin-state.png)
- On the `Output` tab, uncheck the option for `Filter output with OutputPath` and check the option for `Transform result with ResultSelector` then paste the following json in the textbox
  :::code{showCopyAction=true language=json}
  {
  "max.$": "$.Payload.max",
  "min.$": "$.Payload.min"
  }
  :::
  ![Output Max Min State](/static/img/module-7/module-7-output-maxmin-state.png)

10. Click on **Next** and review the generate code and click **Next** again.

- Provide a name to this state machine. For example: `ParallelProcessing-sm`. Choose the provided IAM role with the name containing `StepFunctionsIamRole`.
- You can leave the rest of the defaults and click on **Create state machine**.
  Congratulations, you have a state machine that can run basic calculations in parallel over a data set. Copy the ARN of the State Machine and save it somewhere, you will need it to test the integration with API Gateway.

Next step is to setup the integration with API Gateway.

## Setting up the integration between API Gateway and Step Functions

1. Go to the API Gateway console and select the API already created for this activity.
   ![API Console](/static/img/module-7/module-7-API-console.png)
2. From the list of resources find the execution resource and click on `POST`
   ![API Execution](/static/img/module-7/module-7-API-execution.png)
3. Click on `Integration Request`
4. For the `Integration type` select `AWS Service`
5. Let's configure the integration:

- **AWS Region**: select the AWS regions where you created the State Machine
- **AWS Service**: select `Step Functions` from the dropdown
- **HTTP Method**: select `POST`
- **Action Type**: select `Use action name`
- **Action**: type `StartExecution`
- **Execution role**: find in IAM the role with `IntegrationIamRole` in its name and use the ARN of such role
  ![API Integration Setup](/static/img/module-7/module-7-API-integration-setup.png)
- Click `Save`, when prompted if you are sure that you want to switch the integration click `Ok`
  Congratulations! You just setup an integration between API Gateway and Step Functions without a single line of code.

**Next step**: testing.
