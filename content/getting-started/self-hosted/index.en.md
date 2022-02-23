---
title: 'Self Hosted'
weight: 22
---

:::alert{header="Important" type="warning"}
Only complete this section if you would like to run this workshop **in your own account**. If you are participating in an AWS Event using the Event Engine, [click here](../event-engine).
:::

### Launch the AWS CloudFormation template

This workshop can be run inside your own AWS accounts. To enable you to follow the labs, we need to set up and configure a number of AWS services. We have made provisioning these services as simple as possible
:::alert{type="warning"}
By executing these templates, you are taking responsibility for the lifecycle and costs associated with provisioning them. Please follow the **Clean up** to remove all resources from your AWS account once you have finished the workshop to avoid incurring unexpected costs.
:::
We will leverage AWS CloudFormation which allows us to codify our infrastructure. Select your preferred region to which you will deploy the template. Just click the Launch link for any one of the regions provided below to create the stack in your account.

::::tabs{variant="container" activeTabId="us-east-1"}
:::tab{id="us-east-1" label="us-east-1"}
[US East (N. Virginia)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?stackName=aws-step-functions-workshop&templateURL=https://s3.amazonaws.com/ws-assets-us-east-1/9e0368c0-8c49-4bec-a210-8480b51a34ac/consolidated.yml)
:::
:::tab{id="us-west-2" label="us-west-2"}
[US West (Oregon)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?stackName=aws-step-functions-workshop&templateURL=https://serverless-microservices-orchestration-aws-step-functions-workshop-assets.s3.amazonaws.com/consolidated.yml)
:::
:::tab{id="eu-west-1" label="eu-west-1"}
[Europe (Ireland)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/review?stackName=aws-step-functions-workshop&templateURL=https://serverless-microservices-orchestration-aws-step-functions-workshop-assets.s3.amazonaws.com/consolidated.yml)
:::
:::tab{id="eu-central-1" label="eu-central-1"}
[Europe (Frankfurt)](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?stackName=aws-step-functions-workshop&templateURL=https://serverless-microservices-orchestration-aws-step-functions-workshop-assets.s3.amazonaws.com/consolidated.yml)
:::
:::tab{id="ap-southeast-1" label="ap-southeast-1"}
[Asia Pacific (Singapore)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/review?stackName=aws-step-functions-workshop&templateURL=https://serverless-microservices-orchestration-aws-step-functions-workshop-assets.s3.amazonaws.com/consolidated.yml)
:::
:::tab{id="ap-southeast-2" label="ap-southeast-2"}
[Asia Pacific (Sydney)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/review?stackName=aws-step-functions-workshop&templateURL=https://serverless-microservices-orchestration-aws-step-functions-workshop-assets.s3.amazonaws.com/consolidated.yml)
:::
::::

1. Enter a stack name (or just keep the default name)
2. **Check** the boxes in the Capabilities section
3. Click **Create stack**
