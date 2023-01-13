---
title: 'AWS SAM et configuration du projet'
weight: 134
---

L'environnement AWS Cloud9 est fourni avec certains utilitaires AWS préinstallés. Exécutez la commande suivante dans votre terminal AWS Cloud9 pour vérifier qu'il contient une version mise à jour d'AWS SAM. La version devrait être au moins v1.3X.

```bash
sam --version
```

### Configurer votre dossier et vos fichiers AWS SAM
```bash
mkdir stepfunctions-rest-api-sam
cd stepfunctions-rest-api-sam
```

Créez trois fichiers dans ce projet avec la commande suivante :

```bash
touch template.yaml api.yaml hello_world.asl.yaml
```

- `template.yaml` - Ce fichier est le fichier de configuration AWS SAM principal. Les modèles AWS SAM sont une extension des modèles AWS CloudFormation, avec quelques composants supplémentaires qui facilitent leur utilisation. Pour obtenir la référence complète des modèles AWS CloudFormation, consultez [AWS CloudFormation Template Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html) dans le Guide de l'utilisateur AWS CloudFormation.

- `api.yaml` - Ce fichier est le fichier de définition [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.1.md) qui configurera la structure du endpoint API Gateway.

- `hello_world.asl.yaml` - Ce fichier est le [Amazon States Language (ASL)](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html ) fichier de définition qui configurera le workflow pour votre machine à états Step Functions.


### Utiliser AWS SAM pour créer une REST API Gateway avec integration à Synchronous Express State Machine

Tout d'abord, vous allez passer en revue les extraits de code de chaque fichier de ce projet. Vous allez copier/coller ces extraits dans les fichiers appropriés. Ensuite, vous utiliserez SAM pour générer et déployer le projet. Enfin, vous testerez le déploiement.

#### Examiner le modèle SAM

Passez en revue l'extrait de code ci-dessous. Ce code appartient à votre fichier de modèle SAM `template.yaml`. Notez que ce fichier yaml définit plusieurs ressources, dont une [`AWS::Serverless::Api`](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-api. html) et une [`AWS::Serverless::StateMachine`](https://docs.aws.amazon.com/serverless-application-model/latest/eveloperguide/sam-resource-statemachine.html) avec le type `EXPRESS`. Notez les références aux deux fichiers de définition supplémentaires : `api.yaml` et `hello_world.asl.yaml`. Notez que le template définit deux rôles IAM.

Passez en revue le code, puis copiez/collez-le dans le fichier `template.yaml`.

```yaml
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

#### Revoir la définition ASL

Passez en revue l'extrait de code ci-dessous. Ce code appartient à votre fichier de définition ASL `hello_world.asl.yaml`. Ce workflow contient un seul état `Pass` et renvoie la valeur `Hello back to you!`.

Passez en revue le code, puis copiez/collez-le dans le fichier `hello_world.asl.yaml`.

```json
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

#### Examinez le fichier de mappage api.yaml

Passez en revue l'extrait de code ci-dessous. Ce code appartient à votre fichier de définition OpenAPI `api.yaml`. Ce fichier définit un chemin de publication unique configuré pour invoquer `HelloWorldStateMachine`.

Passez en revue le code, puis copiez/collez-le dans le fichier `api.yaml`.

```yaml
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

#### Déployer le projet

Pour déployer Amazon API Gateway et la machine à états AWS Step Functions sur votre compte AWS, exécutez les commandes suivantes à partir de la racine de l'application :

```bash
sam build
sam deploy --guided
```
![AWS SAM deploy](/static/img/module-11/sam-deploy.png)

Une fois le déploiement terminé, AWS SAM affichera l'URL de l'API REST en sortie. Copiez cette URL. Vous l'utiliserez pour tester l'application à l'étape suivante.