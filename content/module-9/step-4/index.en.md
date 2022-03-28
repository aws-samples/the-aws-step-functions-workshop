---
title: 'Clean up'
weight: 113
---

### CDK project clean up

:::alert{header="Important" type="warning"}
Follow the instructions below only if you are trying this in your own account.
:::

When you're done trying out your API Gateway, you can destroy both the state machine and the API Gateway using the AWS CDK. Issue `cdk destroy` in your app's main directory.

When it is complete you will see the success message below:
![CDK Destroy](/static/img/module-9/cdk-destroy.png)

### Cloud9 clean up

- Select the `stepfunctionsworkshop` Cloud9 environment and then click on Delete. 
- Confirm by typing `Delete` in the text box provided.

### IAM Role clean up

- Go to IAM console
- Select (or search for) the role - **stepfunctionsworkshop-admin**
- Click Delete
