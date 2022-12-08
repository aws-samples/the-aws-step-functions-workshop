---
title: 'AWS SAM and Project Setup'
weight: 134
---

The AWS Cloud9 environment comes with some AWS utilities pre-installed. Run the following command in your AWS Cloud9 terminal to verify that it contains an updated version of AWS SAM. It should be at least v1.3X.

```bash
sam --version
```

### Set up your AWS SAM Project Folder and Files

```bash
mkdir stepfunctions-rest-api-sam
cd stepfunctions-rest-api-sam
```

Create three files in this project with the following command:

```bash
touch template.yaml api.yaml hello_world.asl.json
```

- `template.yaml` - This file is the primary AWS SAM configuration file. AWS SAM templates are an extension of AWS CloudFormation templates, with some additional components that make them easier to work with. For the full reference for AWS CloudFormation templates, see [AWS CloudFormation Template Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html) in the AWS CloudFormation User Guide.

- `api.yaml` - This file is the [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.1.md) definition file that will configure the structure of the API Gateway endpoint.

- `hello_world.asl.json` - This file is the [Amazon States Language (ASL)](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) definition file that will configure the workflow for your Step Functions state machine.

### Use AWS SAM to create an API Gateway REST API with Synchronous Express State Machine backend integration

First, you'll review code snippets for each file in this project. You'll copy/paste these snippets into the appropriate files. Then you will use SAM to build and deploy the project. Last you will test the deployment.

#### Review the SAM template

Review the code snippet below. This code belongs in your SAM template file `template.yaml`. Notice that this yaml file defines several resources including a [`AWS::Serverless::Api`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-api.html) and a [`AWS::Serverless::StateMachine`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-statemachine.html) with the type `EXPRESS`. Notice references to the two additional definition files: `api.yaml` and `hello_world.asl.json`. Notice that the file defines two IAM roles.

Review the code and then copy/paste it into the `template.yaml` file.

```bash
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: >
  stepfunctions-rest-api

  Sample SAM Template for stepfunctions-rest-api

# More info about Globals: https://github.com/awslabs/serverless-application-model/blob/master/docs/globals.rst
Globals:
  Function:
    Timeout: 3

Resources:

  HelloWorldApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: dev
      DefinitionBody:
        'Fn::Transform':
          Name: 'AWS::Include'
          Parameters:
            Location: 'api.yaml'

  HelloWorldStateMachine:
    Type: AWS::Serverless::StateMachine
    Properties:
      DefinitionUri: hello_world.asl.json
      Role: !GetAtt HelloWorldStateMachineRole.Arn
      Type: EXPRESS

  RestApiRole:
    Type: 'AWS::IAM::Role'
    Properties:
      AssumeRolePolicyDocument:
        Version: 2012-10-17
        Statement:
          - Effect: Allow
            Principal:
              Service:
              - apigateway.amazonaws.com
            Action:
              - 'sts:AssumeRole'
      Policies:
      - PolicyName: AllowSFNExec
        PolicyDocument:
          Version: 2012-10-17
          Statement:
            - Effect: Allow
              Action: "states:StartSyncExecution"
              Resource: !GetAtt HelloWorldStateMachine.Arn
  HelloWorldStateMachineRole:
    Type: 'AWS::IAM::Role'
    Properties:
      AssumeRolePolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: Allow
            Principal:
              Service:
                - !Sub states.${AWS::Region}.amazonaws.com
            Action: sts:AssumeRole
Outputs:
  HelloWorldApi:
    Description: "API Gateway endpoint URL to call Hello World State Machine"
    Value: !Sub "https://${HelloWorldApi}.execute-api.${AWS::Region}.amazonaws.com/dev/"
  HelloWorldStateMachineArn:
    Description: "Hello World State Machine ARN"
    Value: !Ref HelloWorldStateMachine
  HelloWorldStateMachineRole:
    Description: "IAM Role created for Hello World State Machine based on the specified SAM Policy Templates"
    Value: !GetAtt HelloWorldStateMachineRole.Arn
```

#### Review the ASL definition

Review the code snippet below. This code belongs in your ASL definition file `hello_world.asl.json`. This workflow contains a single `Pass` state and returns the value "Hello back to you!".

Review the code and then copy/paste it into the `hello_world.asl.json` file.

```bash
  {
    "Comment": "A description of my state machine",
    "StartAt": "Pass",
    "States": {
      "Pass": {
        "Type": "Pass",
        "End": true,
        "Result": {
          "value": "Hello back to you!"
        }
      }
    }
  }
```

#### Review the api.yaml mapping file

Review the code snippet below. This code belongs in your OpenAPI definition file `api.yaml`. This file defines a single post path configured to invoke the `HelloWorldStateMachine`.

Review the code and then copy/paste it into the `api.yaml` file.

```bash
openapi: "3.0.1"
info:
  title: "SAMStepFunctionsRestApi"
  version: "1.0"
paths:
  /:
    post:
      responses:
        "400":
          description: "400 response"
          content: {}
        "200":
          description: "200 response"
          content: {}
      x-amazon-apigateway-integration:
        credentials:
          Fn::GetAtt: [RestApiRole, Arn]
        httpMethod: "ANY"
        uri:
          Fn::Sub: arn:aws:apigateway:${AWS::Region}:states:action/StartSyncExecution
        responses:
          "200":
            statusCode: "200"
            responseTemplates:
              application/json: "{\"output\":$input.json('$.output')}"
          "400":
            statusCode: "400"
        requestTemplates:
          application/json:
             Fn::Sub:
                "{\"input\": \"$util.escapeJavaScript($input.json('$'))\"\
                , \"stateMachineArn\": \"${HelloWorldStateMachine}\"\
                }"
        passthroughBehavior: "when_no_match"
        type: "aws"
components: {}
```

::alert[Cloud9 does not automatically save your files so be sure to save them]{header="Save your files!"}

#### Deploy the project

To deploy the Amazon API Gateway and the AWS Step Functions state machine to your AWS account, run the following commands from the application root:

```bash
sam build
sam deploy --guided
```

![AWS SAM deploy](/static/img/module-11/sam-deploy.png)

After completing the deployment, AWS SAM will display the REST API url as output. Copy this url. You will use it to the test the application in the next step.
