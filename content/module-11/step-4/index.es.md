---
title: 'AWS SAM y configuración de proyecto'
weight: 134
---

El entorno AWS Cloud9 viene con algunas utilidades AWS preinstaladas. Ejecuta el siguiente comando en tu terminal AWS Cloud9 para verificar que contiene una versión actualizada de AWS SAM. Debería ser al menos v1.3X.

```bash
sam --version
```

### Configura tu carpeta y archivos de proyecto de AWS SAM

```bash
mkdir stepfunctions-rest-api-sam
cd stepfunctions-rest-api-sam
```

Crea tres archivos en este proyecto con el siguiente comando:

```bash
touch template.yaml api.yaml hello_world.asl.json
```

- `template.yaml` - Este archivo es el archivo de configuración principal de AWS SAM. Los plantillas de AWS SAM son una extensión de las plantillas de AWS CloudFormation, con algunos componentes adicionales que las hacen más fáciles de trabajar. Para la referencia completa de las plantillas de AWS CloudFormation, consulta [Referencia de plantillas de AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html) en la Guía del usuario de AWS CloudFormation.

- `api.yaml` - Este archivo es el archivo de definición de [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.1.md) que configurará la estructura de la API.

- `hello_world.asl.json` - Este archivo es el archivo de definición de [Amazon States Language (ASL)](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) que configurará el flujo de trabajo de tu máquina de estado de Step Functions.

### Utiliza AWS SAM para crear una API REST integrando un máquina de estado de Express síncrona

Primero, revisará fragmentos de código para cada archivo en este proyecto. Copiarás y pegarás estos fragmentos en los archivos adecuados. Luego usarás SAM para construir y desplegar el proyecto. Finalmente, probarás el despliegue.

#### Revisar la plantilla SAM

Revisa el fragmento de código a continuación. Este código pertenece a tu archivo de plantilla SAM `template.yaml`. Observa que este archivo yaml define varios recursos, incluyendo un [`AWS::Serverless::Api`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-api.html) y un [`AWS::Serverless::StateMachine`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-statemachine.html) con el tipo `EXPRESS`. Observa las referencias a los dos archivos de definición adicionales: `api.yaml` y `hello_world.asl.json`. Observa que el archivo define dos roles de IAM.

Revisa el código, luego cópiealo y pégalo en el archivo `template.yaml`.

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

#### Revisa la definición de ASL

Revisa el fragmento de código a continuación. Este código pertenece a tu archivo de definición ASL `hello_world.asl.json`. Este flujo de trabajo contiene un único estado `Pass` y devuelve el valor "Hello back to you!".

Revisa el código, luego cópialo y pégalo en el archivo `hello_world.asl.json`.

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

#### Revisa el archivo de mapeo api.yaml

Revisa el fragmento de código a continuación. Este código pertenece a tu archivo de definición OpenAPI `api.yaml`. Este archivo define un único método POST configurado para invocar la máquina de estados `HelloWorldStateMachine`.

Revisa el código, luego cópialo y pégalo en el archivo `api.yaml`.

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

::alert[Cloud9 no guarda automáticamente tus archivos, así que asegúrate de guardarlos]{header="¡Guarda tus archivos!"}

#### Desplegar el proyecto

Para desplegar Amazon API Gateway y la máquina de estados AWS Step Functions en tu cuenta de AWS, ejecuta los siguientes comandos desde la raíz de la aplicación:

```bash
sam build
sam deploy --guided
```

![AWS SAM deploy](/static/img/module-11/sam-deploy.png)

Después de completar el despliegue, AWS SAM mostrará la url de la API REST como salida. Copia esta url. La usarás para probar la aplicación en el siguiente paso.
