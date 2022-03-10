---
title: 'Setup'
weight: 31
---

:::alert{header="Important" type="warning"}
Follow the instructions on this page only if you are trying this in your own account. Otherwise, [click here](../step-2) to get started
:::

- Run the command given below to download the CloudFormation template to your local machine.

```bash
curl ':assetUrl{path="/resources/module_1.yml"}' --output module_1.yml
```

::::tabs{variant="container"}
:::tab{id="us-east-1" label="N. Virginia"}
[US East - Launch](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
:::tab{id="us-west-2" label="Oregon"}
[US West - Launch](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
:::tab{id="eu-west-1" label="Ireland"}
[Europe West - Launch](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
:::tab{id="eu-central-1" label="Frankfurt"}
[Europe Central - Launch](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
:::tab{id="ap-southeast-1" label="Singapore"}
[Asia Pacific South East - Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
:::tab{id="ap-southeast-2" label="Sydney"}
[Asia Pacific South East - Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
:::tab{id="ap-northeast-1" label="Tokyo"}
[Asia Pacific North East - Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=:assetUrl{path="/resources/module_1.yml"})
:::
::::

- Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=us-east-1) page in the AWS Console.
- Click on _Create stack -> With new resources (standard)_ as shown below
  ![CloudFormation home page](/static/img/setup/setup-cloudformation-homepage.png)
- On the _Create stack_ page, select _Upload a template file_ and then click on `Choose File` button. Select the file saved from the previous step.
  ![CloudFormation choose file](/static/img/setup/setup-cloudformation-choose-file.png)
- On the _Specify stack details_ page, specify _Stack name_ e.g. `SFW-Module-1`
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Click _Next_ two times and on the last `Review` page, scroll to the bottom. Click the checkbox shown and then click `Create stack`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Wait till the stack shows `CREATE_COMPLETE` status.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)
