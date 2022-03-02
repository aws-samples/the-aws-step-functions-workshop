---
title: 'Clean up'
weight: 85
---

## Manually delete the state machine

Navigate to **Step Functions**
If you have named the state machines as per the instructions provided

- select **Lambda-input-output-processing-sm** from the list of state machines.
- Click **Delete** button
- Confirm by clicking **Delete state machine** button on the dialog box that is displayed.

:::alert{header="Important" type="warning"}
Follow the instructions given below only if you are trying this in your own account.
:::

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=us-east-1) page in the AWS Console.
- Select the stack with name `SFW-Module-6` (or any name you have chosen for the stack) and then click Delete.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.
