---
title: 'AWS SAM and Project Setup'
weight: 124
---

The AWS Cloud9 environment comes with some AWS utilities pre-installed. Run the following command in your AWS Cloud9 terminal to verify that it contains an updated version of AWS SAM. It should be at least v1.3X.

```bash
sam --version
```

### Set up your AWS SAM Project
```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
```

### Use AWS SAM to create an API Gateway REST API with Synchronous Express State Machine backend integration

First, we'll review the individual code snippets that define the Synchronous Express State Machine and the API Gateway REST API. Later we will put them together into an AWS SAM app. Then we will build and deploy these resources. 

#### Review the Step Functions state machine definition

This AWS SAM resource defines the configuration of a simple state machine.
```bash
  HelloWorldStateMachine:
    Type: AWS::Serverless::StateMachine
    Properties:
      DefinitionUri: hello_world.asl.json
      Role: !GetAtt HelloWorldStateMachineRole.Arn
      Type: EXPRESS
  HelloWorldStateMachineRole:
    Type: AWS::IAM::Role
    Properties:
      AssumeRolePolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: Allow
            Principal:
              Service:
                - !Sub states.${AWS::Region}.amazonaws.com
            Action: sts:AssumeRole
```
Notice the snippet above contains
- The State Machine definition is in the `hello_world.asl.json` file
- The State Machine's IAM role is `HelloWorldStateMachineRole`
- The State Machine Type is `EXPRESS`

This Amazon States Language code will be in the `hello_world.asl.json` file. Review this code now.

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

Notice the snippet above contains a `Pass` state named `PassState` that returns a string "Hello back to you!". Add the snippet to a new file called `hello_world.asl.json`.

#### Review the API Gateway REST API definition

Next we will use `AWS::Serverless::Api` construct to create the API Gateway REST API with required permissions and reference the input/output mapping in the `api.yaml` file. We can use this definition to create an integration between the state machine and API Gateway.

```bash
  HelloWorldApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: dev
      DefinitionBody:
        'Fn::Transform':
          Name: 'AWS::Include'
          Parameters:
            Location: 'api.yaml'
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
```

#### Review the api.yaml mapping file
```
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
The `api.yaml` file defines the request and response mapping for the API and connects the API Gateway to the Step Functions state machine. Add the snippet above to a new file called `api.yaml`.

#### Put it together

In the AWS SAM project, replace the contents of the `template.yaml` file with the code below. You'll recognize the definitions of the Step Functions state machine and the API Gateway.

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
    Type: AWS::IAM::Role
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

Save the template file. To deploy the Amazon API Gateway and the AWS Step Functions state machine to your AWS account, run the following commands from the application root:

```bash
sam build
sam deploy --guided
```
![AWS CDK diagram](/static/img/module-10/sam-deploy.png)

After completing the deployment, AWS SAM will display the REST API url as output. Copy this url. You will use it to the test the application in the next step.