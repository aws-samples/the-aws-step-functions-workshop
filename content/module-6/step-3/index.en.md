---
title: 'Build a state machine using Workflow Studio'
weight: 82
---

A simple lambda function called `HelloFunction` is already created for you in your AWS account. Follow the below steps to create a simple workflow using Workflow Studio.

1. Navigate to Step Functions in your AWS console. Make sure you are in the same AWS region that is assigned for this session.

2. If you are not on the `State machines` page, click on `State machines` on the left side menu and click **Create state machine**

3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Standard** and click on `Next`.
   ![Studio](/static/img/module-6/extra-credit-2-studio-selection.png)

4. You should see the designer studio now which will look like this.
   ![](/static/img/module-6/extra-credit-2-studio-designer.png)

5. For `Comment` on the right side, enter `A step functions example showing input and output processing`.

6. Drag & drop `AWS Lambda` from the **Actions** section on the left side to the designer form where it says `Drag first state here`.
   ![](/static/img/module-6/extra-credit-2-lambda-invoke-state.png)

7. Lets configure the state.

- On the `Configuration` tab of the designer, enter `HelloFunctionWorkflow` for state name.
- In the API parameters section, select `HelloFunction` from the drop down of **Function name**
  ![](/static/img/module-6/extra-credit-2-configuration.png)
- Click on `Input` tab and check the box for `filter input with InputPath - optional`. Enter `$.lambda` for the value.
  ![](/static/img/module-6/extra-credit-2-config-input.png)
- Click on the `Output` tab and enter `$.data.lambdaresult` for the `ResultPath`. Leave the selection as `Combine original input with result`.
- Check the box for `Filter output with OutputPath` and enter `$.data` for the value.
  ![](/static/img/module-6/extra-credit-2-config-output.png)
- Click on `Error handling` tab and delete the retrier pre-added to the **Retry on errors**.
  ![](/static/img/module-6/extra-credit-2-error-handling.png)
- Click on **Next** and review the generate code and click **Next** again.
- Provide a name to this state machine. For example: `Lambda-input-output-processing-sm`. For the IAM role, select an existing IAM role `InputOuputProcessingStepFuntionRole`
  ![](/static/img/module-6/extra-credit-2-name-iam-role.png)
- You can leave the rest of the defaults and click on **Create state machine**.
