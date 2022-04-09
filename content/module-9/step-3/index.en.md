---
title: 'CDK and Project Setup'
weight: 113
---

The Cloud9 environment comes with some AWS utilities pre-installed. Run the following command in your Cloud9 terminal to verify that it contains an updated version of AWS CDK. It should be v2.x.

```bash
cdk --version
```

### Bootstrapping AWS CDK

Deploying AWS CDK apps into an AWS environment may require that you provision resources the AWS CDK needs to perform the deployment. These resources include an Amazon S3 bucket for storing files and IAM roles that grant permissions needed to perform deployments. The process of provisioning these initial resources is called bootstrapping. This typically needs to be done once per region in a given account.

```bash
cdk bootstrap aws://${AWS_ACCOUNT_ID}/${AWS_REGION}
```

### Set Up Your AWS CDK Project

Create a new directory for the AWS CDK app and initialize the project.

```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
cdk init --language typescript
```

::alert[Be sure to name the directory `stepfunctions-rest-api`. The AWS CDK application template uses the name of the directory to generate names for source files and classes. If you use a different name, your app will not match this tutorial.]{header="Note"}

### Use AWS CDK to create an API Gateway REST API with Synchronous Express State Machine backend integration

First, we'll review the individual code snippets that define the Synchronous Express State Machine and the API Gateway REST API. Later we will put them together into an AWS CDK app. Last we will synthesize and deploy these resources. The code is written in TypeScript.

#### Review the Step Functions state machine definition

This AWS CDK code defines a simple state machine with a `pass` state.

```bash
const machineDefinition = new sfn.Pass(this, 'PassState', {
    result: {value:"Hello!"},
})

const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
    definition: machineDefinition,
    stateMachineType: stepfunctions.StateMachineType.EXPRESS,
});
```

This snippet contains:

- A machine definition named `PassState`, which is a `pass` state.
- The state machine’s logical name: `MyStateMachine`.
- The machine definition is set as the StateMachine definition.
- The StateMachineType is set as `EXPRESS`. `StepFunctionsRestApi` will only allow a Synchronous Express state machine.

#### Review the API Gateway REST API definition

Next we will use `StepFunctionsRestApi` construct to create the API Gateway REST API with required permissions and default input/output mapping. This is a high level construct which contains many pre-defined configurations. We can use this definition to create an integration between the state machine and API Gateway.

```bash
const api = new apigateway.StepFunctionsRestApi(this, 'StepFunctionsRestApi', { stateMachine: stateMachine });
```

#### Put it together

In the AWS CDK project, replace the contents of the `lib/stepfunctions-rest-api-stack.ts` file with the code below. You'll recognize the definitions of the Step Functions state machine and the API Gateway.

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

Replace the contents of `bin/stepfunctions-rest-api.ts` with the code below.

```bash
#!/usr/bin/env node
import 'source-map-support/register';
import * as cdk from 'aws-cdk-lib';
import { StepfunctionsRestApiStack } from '../lib/stepfunctions-rest-api-stack';

const app = new cdk.App();
new StepfunctionsRestApiStack(app, 'StepfunctionsRestApiStack');
```

Save these source files. From the terminal run `cdk synth` from the main directory. The `cdk synth` command executes the app, which causes the resources defined in it to be translated into an AWS CloudFormation template.

To deploy the Amazon API Gateway and the AWS Step Functions state machine to your AWS account, run the `cdk deploy` command. You'll be asked to approve the IAM policies the AWS CDK has generated.

After completing the deployment, CDK will display the REST API url as output. Please make a note of this as you will use it to the test the setup in the next step.
