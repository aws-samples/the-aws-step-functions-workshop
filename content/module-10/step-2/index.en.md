---
title: 'Setup'
weight: 122
---

:::alert{header="Important" type="warning"}
Follow the instructions on this page only if you are executing this workshop in your own account. To skip these instructions [click here](../step-3).
:::

- Click on the `Launch` link against any of the regions in the table below to start the deployment.
  | Region | Launch stack |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |
  | **Europe (Ireland)** eu-west-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |

- Location of the CloudFormation template will be auto populated in the `Amazon S3 URL` field as shown in the diagram below. Click `Next`
  ![CloudFormation specify template](/static/img/setup/setup-cloudformation-specify-template.png)
- On the _Specify stack details_ page, _Stack name_ would be auto populated to `SFW-Module-10`. You can specify a different name if you want.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Click _Next_ two times and on the last `Review` page, scroll to the bottom. Click the checkbox `if shown` and then click `Create stack`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Wait till the stack shows `CREATE_COMPLETE` status.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)
