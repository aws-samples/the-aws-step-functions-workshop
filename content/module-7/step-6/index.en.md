---
title: 'Clean up'
weight: 96
---

## Manually delete the state machine

Navigate to **Step Functions**
If you have named the state machines as per the instructions provided

- select **ParallelProcessing-sm** from the list of state machines.
- Click **Delete** button
- Confirm by clicking **Delete state machine** button on the dialog box that is displayed.
  ![Statemachine delete](/static/img/module-7/module-7-manual-delete-sm.png)

If you have chosen different names while creating the state machines, follow the above instructions while selecting the appropriate state machines.

:::alert{header="Important" type="warning"}
Follow the instructions given below only if you are trying this in your own account.
:::

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=us-east-1) page in the AWS Console.
- Select the stack with name `SFW-Module-7` (or any name you have chosen for the stack) and then click Delete.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.
