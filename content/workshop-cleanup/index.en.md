---
title: 'Workshop cleanup'
weight: 120
---

:::alert{type="warning"}
**Only complete this section if you are Self Hosting this workshop.** If you are running this workshop at an AWS hosted event, such as re\:Invent, Loft, Immersion Day, or any other event hosted by an AWS employee, you skip this section, as we will clean up everything for you.
:::

## Manually delete the state machines created during Modules 6 and 7

Navigate to **Step Functions**
If you have named the state machines as per the instructions provided in modules 6 and 7 then

- select **Lambda-input-output-processing-sm** from the list of state machines.
- Click **Delete** button
- Confirm by clicking **Delete state machine** button on the dialog box that is displayed.
  Repeat the above steps for **UniversalSDKIntegration-sm**.

If you have chosen different names while creating the state machines, follow the above instructions while selecting the appropriate state machines.

## Delete the workshop CloudFormation stack

Once you have deleted the manually created state machines in the previous steps (if required), delete the CloudFormation Stack for the workshop. This will remove all resource created for the workshop from your account.

1. Select the stack as shown in the picture below
2. Click the **Delete** button to delete the stack

![Delete Stack](/static/cleanup_cloud_formation_delete.png)
::alert[**That's It, All Done!** You have successfully completed the workshop.]{type="success"}
