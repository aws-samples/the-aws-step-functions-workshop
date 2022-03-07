---
title: 'CDK and Project Setup'
weight: 112
---

Cloud9 environment comes pre-built with some of the AWS utilities.

Run the following command in your Cloud9 environment to verify correct installation and print the version of AWS CDK. You should see v2.x.

```bash
cdk --version
```

### Bootstrapping AWS CDK

Many AWS CDK stacks that you write will include assets: external files that are deployed with the stack, such as AWS Lambda functions or Docker images. The AWS CDK uploads these to an Amazon S3 bucket or other container so they are available to AWS CloudFormation during deployment. Deployment requires that these containers already exist in the account and region you are deploying into. Creating them is called bootstrapping. To bootstrap, issue:

```bash
cdk bootstrap aws://${AWS_ACCOUNT_ID}/${AWS_REGION}
```

Wait for the above script to finish executing and bootstrapping the environment

### Set Up Your AWS CDK Project

First, create a directory for your new AWS CDK app and initialize the project.

```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
cdk init --language typescript
```

::alert[Be sure to name the directory `stepfunctions-rest-api`. The AWS CDK application template uses the name of the directory to generate names for source files and classes. If you use a different name, your app will not match this tutorial.]{header="Note"}

### Use the AWS CDK to create an API Gateway REST API with Synchronous Express State Machine backend integration

First, we'll present the individual pieces of code that define the Synchronous Express State Machine and the API Gateway REST API, then explain how to put them together into your AWS CDK app. Then you'll see how to synthesize and deploy these resources.

::alert[The State Machine that we will show here will be a simple State Machine with a Pass state.]{header="Note"}

This is the AWS CDK code that defines a simple state machine with a `Pass` state.

```bash
const machineDefinition = new sfn.Pass(this, 'PassState', {
    result: {value:"Hello!"},
})

const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
    definition: machineDefinition,
    stateMachineType: stepfunctions.StateMachineType.EXPRESS,
});
```

You can see in this short snippet:

- The machine definition named `PassState`, which is a `Pass` State.
- The State Machine’s logical name, `MyStateMachine`.
- The machine definition is used as the State Machine definition.
- The State Machine Type is set as `EXPRESS` because `StepFunctionsRestApi` will only allow a Synchronous Express state machine.

Next we will use StepFunctionsRestApi construct to create the API Gateway REST API with required permissions and default input/output mapping. This is a higher level construct which does a lot of things behind the scenes and integrates state machine with the API Gateway.

```bash
const api = new apigateway.StepFunctionsRestApi(this, 'StepFunctionsRestApi', { stateMachine: stateMachine });
```

In the AWS CDK project you created, edit the file containing the definition of the stack to look like the code below. You'll recognize the definitions of the Step Functions state machine and the API Gateway from above.

Update `lib/stepfunctions-rest-api-stack.ts` to read as follows.

```bash
import * as cdk from 'aws-cdk-lib';
import * as stepfunctions from 'aws-cdk-lib/aws-stepfunctions';
import * as apigateway from 'aws-cdk-lib/aws-apigateway';

export class StepfunctionsRestApiStack extends cdk.Stack {
    constructor(app: cdk.App, id: string) {
      super(app, id);

      const machineDefinition = new stepfunctions.Pass(this, 'PassState', {
          result: {value:"Hello!"},
      })

      const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
          definition: machineDefinition,
          stateMachineType: stepfunctions.StateMachineType.EXPRESS,
      });

      const api = new apigateway.StepFunctionsRestApi(this, 'StepFunctionsRestApi', { stateMachine: stateMachine });
    }
}
```

Update `bin/stepfunctions-rest-api.ts` to read as follows.

```bash
#!/usr/bin/env node
import 'source-map-support/register';
import * as cdk from 'aws-cdk-lib';
import { StepfunctionsRestApiStack } from '../lib/stepfunctions-rest-api-stack';

const app = new cdk.App();
new StepfunctionsRestApiStack(app, 'StepfunctionsRestApiStack');
```

Save the source file, then issue `cdk synth` in the app's main directory. The AWS CDK runs the app and synthesizes an AWS CloudFormation template from it, then displays the template.

To actually deploy the Amazon API Gateway and the AWS Step Functions state machine to your AWS account, issue `cdk deploy`. You'll be asked to approve the IAM policies the AWS CDK has generated.

After completing the deployment, CDK will display the REST API url as output. Please make a note of this as you will use it to the test the setup in the next step.
