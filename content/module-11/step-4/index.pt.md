---
title: 'AWS SAM e Configuração do Projeto'
weight: 134
---

O ambiente AWS Cloud9 vem com alguns utilitários da AWS pré-instalados. Execute o comando a seguir em seu terminal AWS Cloud9 para verificar se ele contém uma versão atualizada do AWS SAM. Deve ser no mínimo v1.3X.

```bash
sam --version
```

### Configure a pasta e os arquivos do seu projeto AWS SAM
```bash
mkdir stepfunctions-rest-api-sam
cd stepfunctions-rest-api-sam
```

Crie três arquivos neste projeto com o seguinte comando:

```bash
touch template.yaml api.yaml hello_world.asl.yaml
```

- `template.yaml` - Esse arquivo é o principal arquivo de configuração do AWS SAM. Os modelos do AWS SAM são uma extensão dos modelos do AWS CloudFormation, com alguns componentes adicionais que facilitam o trabalho com eles. Para obter a referência completa dos modelos do AWS CloudFormation, consulte [AWS CloudFormation Template Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html) no Guia do usuário do AWS CloudFormation..

- `api.yaml` - Esse arquivo é o arquivo de definição do [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.1.md) que configurará a estrutura do endpoint do API Gateway. 

- `hello_world.asl.yaml` - Esse arquivo é o arquivo de definição [Amazon States Language (ASL)](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) que configurará o fluxo de trabalho para sua máquina de estado do Step Functions..


### Use o AWS SAM para criar uma REST API no API Gateway com integração a uma Máquina de estados Expresso Síncrona

Primeiro, você revisará os trechos de código de cada arquivo neste projeto. Você copiará/colará esses trechos nos arquivos apropriados. Em seguida, você usará o SAM para criar e implementar o projeto. Por último, você testará a implementação.

#### Revise o modelo SAM

Revise o trecho de código abaixo. Esse código pertence ao seu arquivo de modelo SAM  `template.yaml`. Observe que esse arquivo yaml define vários recursos, incluindo um [`AWS::Serverless::Api`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-api.html) e uma [`AWS::Serverless::StateMachine`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-statemachine.html) com o tipo `EXPRESS`. Observe as referências aos dois arquivos de definição adicionais: `api.yaml` e `hello_world.asl.yaml`. Observe que o arquivo define duas funções do IAM.

Revise o código e depois copie/cole no arquivo `template.yaml`.

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
      DefinitionUri: hello_world.asl.yaml
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

#### Revise a definição de ASL

Revise o trecho de código abaixo. Esse código pertence ao seu arquivo de definição ASL `hello_world.asl.yaml`.  Esse fluxo de trabalho contém um único estado `Pass` e retorna o valor “Hello back to you! “.

Revise o código e depois copie/cole no arquivo `hello_world.asl.yaml`.

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

#### Examine o arquivo de mapeamento

Revise o trecho de código abaixo. Esse código pertence ao seu arquivo de definição OpenAPI `api.yaml`. Esse arquivo define um único caminho de postagem configurado para invocar o `HelloWorldStateMachine`.

Revise o código e depois copie/cole no arquivo `api.yaml`.

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

#### Implemente o projeto

Para implementar o Amazon API Gateway e a máquina de estado do AWS Step Functions em sua conta AWS, execute os seguintes comandos a partir da raiz do aplicativo:

```bash
sam build
sam deploy --guided
```
![AWS SAM deploy](/static/img/module-11/sam-deploy.png)

Depois de concluir a implementação, o AWS SAM exibirá o URL da REST API como saída. Copie esse URL. Você o usará para testar o aplicativo na próxima etapa.