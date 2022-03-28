---
title: 'Clean up'
weight: 96
---

## Manually delete the state machine

:::alert{header="Important" type="warning"}
Follow the instructions given below only if you are trying this in your own account.
:::

Navigate to **Step Functions**
If you named the state machines per the instructions provided:

- Select **ParallelProcessing-sm** from the list of state machines.
- Click **Delete** button
- Confirm by clicking **Delete state machine** button on the dialog box that is displayed.
  ![Statemachine delete](/static/img/module-7/module-7-manual-delete-sm.png)

If you have chosen different names while creating the state machines, follow the above instructions while selecting the appropriate state machines.


- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) page in the AWS Console.
- Select the stack with name `SFW-Module-7` (or any name you have chosen for the stack) and then click Delete.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.

## Manually delete the CloudWatch log group

Navigate to **CloudWatch** and select **Log groups** under Logs

- select the log group belonging to **ParallelProcessing-sm** step function.
- Click on **Actions** dropdown and then select **Delete log group(s)**.
  ![Cloudwatch loggroup delete](/static/img/module-7/module-7-cloudwatch-cleanup.png)
- Confirm by clicking the **Delete** button in the pop up screen.
