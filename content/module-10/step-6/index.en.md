---
title: 'Clean up'
weight: 126
---

:::alert{header="Important" type="warning"}
Follow the instructions on this page if you would like to clean up resources in your own account. Event Engine accounts do not require cleanup.
:::

### Destroy resources created by CDK

When you have completed testing, you can destroy the API Gateway and the state machine the using AWS CDK. Copy/paste the following command into the terminal in the application's root directory.

```bash
cdk destroy
```

When the `cdk destroy` is complete you will see the following message:
![CDK Destroy](/static/img/module-10/cdk-destroy.png)

### Delete CloudFormation Stack

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home) page in the AWS Console.
- Select the stack with name `SFW-Module-10` (or any name you have chosen for the stack) and then click Delete. This will clean up the AWS Cloud9 environment and any other related resources in the stack.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Make sure the stack deletion completes successfully.
