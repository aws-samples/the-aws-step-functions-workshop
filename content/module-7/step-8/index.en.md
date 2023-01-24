---
title: 'Clean up'
weight: 98
---

:::alert{header="Important" type="warning"}
Follow the instructions on this page if you would like to clean up resources in your own account. Event Engine accounts do not require cleanup.
:::

### Manually delete the state machine

Navigate to **Step Functions**
If you named the state machines per the instructions provided:

- Select **ParallelProcessingMachine** from the list of state machines.
- Click **Delete** button
- Confirm by clicking **Delete state machine** button on the dialog box that is displayed.
  ![Statemachine delete](/static/img/module-7/manual-delete-sm.png)

If you chose a different names for your state machine, follow the instructions above while selecting the appropriate name.

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) page in the AWS Console.
- Select the stack with name `SFW-Module-7` (or any name you have chosen for the stack) and then click Delete.
  ![CloudFormation exclusão](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.

### Manually delete the CloudWatch log group

Navigate to [CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Click **Logs** in the navigation and select **Log groups**.

- select the log group belonging to **ParallelProcessingMachine**.
- Click on **Actions** dropdown and then select **Delete log group(s)**.
  ![Cloudwatch loggroup delete](/static/img/module-7/cloudwatch-cleanup.png)
- Confirm by clicking the **Delete** button in the pop up screen.
