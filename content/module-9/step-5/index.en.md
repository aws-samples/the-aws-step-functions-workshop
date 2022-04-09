---
title: 'Clean up'
weight: 115
---

:::alert{header="Important" type="warning"}
Follow the instructions on this page if you would like to clean up resources in your own account. Event Engine accounts do not require cleanup.
:::

### CDK project clean up

When you're done trying out your API Gateway, you can destroy both the state machine and the API Gateway using the AWS CDK. Issue `cdk destroy` in your app's main directory.

When it is complete you will see the success message below:
![CDK Destroy](/static/img/module-9/cdk-destroy.png)

### Delete CloudFormation Stack

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) page in the AWS Console.
- Select the stack with name `SFW-Module-9` (or any name you have chosen for the stack) and then click Delete.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.
