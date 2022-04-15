---
title: 'AWS CDK and Project Setup'
weight: 114
---

The AWS Cloud9 environment comes with some AWS utilities pre-installed. Run the following command in your AWS Cloud9 terminal to verify that it contains an updated version of AWS CDK. It should be v2.x.

```bash
cdk --version
```

### Bootstrapping AWS CDK

Deploying AWS CDK apps into an AWS environment may require that you provision resources the AWS CDK needs to perform the deployment. These resources include an Amazon S3 bucket for storing files and IAM roles that grant permissions needed to perform deployments. The process of provisioning these initial resources is called bootstrapping. This typically needs to be done once per region in a given account.

```bash
cdk bootstrap aws://${AWS_ACCOUNT_ID}/${AWS_REGION}
```

### Set Up Your AWS CDK Project

Create a new directory for the AWS CDK app and initialize a TypeScript project.

```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
cdk init --language typescript
```

::alert[Be sure to name the directory `stepfunctions-rest-api`. The AWS CDK application template uses the name of the directory to generate names for source files and classes. If you use a different name, your app will not match this tutorial.]{header="Note"}

### Use AWS CDK to create an API Gateway REST API with Synchronous Express State Machine backend integration

First, we'll review the individual code snippets that define the Synchronous Express State Machine and the API Gateway REST API. Later we will put them together into an AWS CDK app. Then we will synthesize and deploy these resources. 

#### Review the Step Functions state machine definition

This AWS CDK code defines a simple state machine with a `pass` state. Review this code now.

```bash
const startState = new sfn.Pass(this, 'PassState', {
    result: {value:"Hello!"},
})

const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
    definition: startState,
    stateMachineType: stepfunctions.StateMachineType.EXPRESS,
});
```

Notice the snippet above contains:

- A `Pass` state construct named `PassState`. 
- A StateMachine construct named `MyStateMachine`.
    -  The StateMachine definition specifies its start state.
    - The stateMachineType is `EXPRESS` (the `StepFunctionsRestApi` construct only allows a Synchronous Express state machine).

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

      const startState = new stepfunctions.Pass(this, 'PassState', {
          result: {value:"Hello back to you!"},
      })

      const stateMachine = new stepfunctions.StateMachine(this, 'CDKStateMachine', {
          definition: startState,
          stateMachineType: stepfunctions.StateMachineType.EXPRESS,
      });

      const api = new apigateway.StepFunctionsRestApi(this, 'CDKStepFunctionsRestApi', { stateMachine: stateMachine });
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
new StepfunctionsRestApiStack(app, 'CDKStepfunctionsRestApiStack');
```

Save these source files. To deploy the Amazon API Gateway and the AWS Step Functions state machine to your AWS account, run the following command from the application root:

```bash
cdk deploy
```

You'll be asked to approve the IAM policies the AWS CDK has generated. After completing the deployment, AWS CDK will display the REST API url as output. Copy this url. You will use it to the test the application in the next step.
