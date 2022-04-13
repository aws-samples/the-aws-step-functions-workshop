---
title: 'Clean up'
weight: 85
---
:::alert{header="Important" type="warning"}
Follow the instructions on this page if you would like to clean up resources in your own account. Event Engine accounts do not require cleanup.
:::

## Manually delete the state machine

Navigate to **Step Functions**
If you named the state machines as per the instructions provided:

- Select **InputOutputProcessingMachine** from the list of state machines.
- Click **Delete** button
- Confirm by clicking **Delete state machine** button on the dialog box that is displayed.

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) page in the AWS Console.
- Select the stack with name `SFW-Module-6` (or any name you have chosen for the stack) and then click Delete.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.
