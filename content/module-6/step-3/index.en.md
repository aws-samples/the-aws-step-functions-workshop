---
title: 'Build a state machine using Workflow Studio'
weight: 82
---

Follow the below steps to create a simple workflow using Workflow Studio.

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in your AWS console. Make sure you are in the correct AWS region.

2. Click the **Create state machine** button.

3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Standard** and click on **Next**.
   ![Studio](/static/img/module-6/studio-selection.png)

4. You should see the designer studio now.
   ![Studio Designer](/static/img/module-6/studio-designer.png)

5. For `Comment` on the right side, enter `A step functions example showing input and output processing`.

6. Drag and drop the **AWS Lambda Invoke** action from the `Actions` section on the left side to the designer form to where it says `Drag first state here`.
   ![Lambda Invoke](/static/img/module-6/lambda-invoke-state.png)

7. Configure the state.

- On the `Configuration` tab of the designer, enter `HelloFunctionWorkflow` for state name.
- You should have a Lambda function called `HelloFunction` already deployed to your acccount.
- Configure this state to invoke that function. Find the `API Parameters` field and click `Enter function name`. Scroll down the menu list until you find **HelloFunction:$LATEST**. Select this value.

![Configuration](/static/img/module-6/configuration.png)

- Click on `Input` tab and check the box for `filter input with InputPath - optional`. Enter `$.lambda` for the value.
  ![Config Input](/static/img/module-6/config-input.png)
- Click on the `Output` tab and check the box to `Add original input to output using ResultPath`. Select `Combine original input with result`. Enter the following string as the ResultPath filter: `$.data.lambdaresult`.
- Check the box to `Filter output with OutputPath` and enter `$.data` for the value.
  ![Config Output](/static/img/module-6/config-output.png)
- Click on the `Error handling` tab. Find the **Retry on errors** section and remove the default `Retrier #1` by clicking the edit icon to the right and scrolling down to click the **Remove** button.
  ![Remove Retrier](/static/img/module-6/remove-retrier.png)
- Click on **Next** and review the generated code and click **Next** again.
- Provide a name to this state machine. For example: `Lambda-input-output-processing-sm`. For the IAM role, select an existing IAM role `InputOutputProcessingStepFunctionRole`
  ![Iam Role](/static/img/module-6/name-iam-role.png)
- You can leave the rest of the defaults and click on **Create state machine**.
