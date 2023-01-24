---
title: 'Localize seus recursos e configure sua máquina de estados'
weight: 74
---

### Localize seus recursos

Navegue até os serviços abaixo no console da AWS para se familiarizar com os recursos. Assegure-se de estar na região correta. Copie o ARN (Amazon Resource Name) do tópico SNS para o bloco de notas, você precisará dele mais tarde neste módulo.

- [AWS Lambda](https://console.aws.amazon.com/lambda/home) - procure **MapStateReadFromSQSQueueLambda** e **MapStateDeleteFromSQSQueueLambda**

- [Amazon SQS](https://console.aws.amazon.com/sqs/v2/home) - procure **MapStateQueueforMessages**

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) - procure **MapStateTable**

- [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) - procure **MapStateTopicforMessages** *(copie o ARN do tópico)*

### Configure sua máquina de estados

1. Navegue para [Step Functions](https://console.aws.amazon.com/states/home) no console AWS.

2. Localize a máquina de estados que contenha **MapStateStateMachine** no seu nome. Clique nela e depois clique em **Edit** no canto direito superior.

![EDIT](/static/img/module-5/map-state-definition-edit.png)

3. Copie a definição do ASL abaixo clicando no ícone quadrado no canto superior direito do exemplo de código. Substitua a definição do ASL na sua máquina de estado com essa copiada. Essa definição possui um total de 4 valores **BLANK** nos campos dos estados Map e Choice. Leia a documentação para saber como atualizar esses valores **BLANK** com a síntaxe de estado correta e seus parâmetros. (Dicas para completar abaixo.)

   - Aprenda sobre a síntaxe do estado [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html).

   - Aprenda sobre [objetos de contexto do estado Map](https://docs.aws.amazon.com/step-functions/latest/dg/input-output-contextobject.html#contextobject-map)
   
   - Aprenda sobre a síntaxe do estado [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html).

```bash
{
  "Comment": "An example of the Amazon States Language for reading messages from an SQS queue and iteratively processing each message.",
  "StartAt": "Read messages from SQS queue",
  "States": {
    "Read messages from SQS queue": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "OutputPath": "$.Payload",
      "Parameters": {
        "FunctionName": "MapStateReadFromSQSQueueLambda"
      },
      "Next": "Are there messages to process?"
    },
    "Are there messages to process?": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "**BLANK**",
          "StringEquals": "No messages",
          "Next": "**BLANK**"
        }
      ],
      "Default": "Process Messages"
    },
    "Process Messages": {
      "Type": "Map",
      "Next": "Finish",
      "ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.**BLANK**",
        "MessageDetails.$": "$$.**BLANK**"
      },
      "Iterator": {
        "StartAt": "Write message to DynamoDB",
        "States": {
          "Write message to DynamoDB": {
            "Type": "Task",
            "Resource": "arn:aws:states:::dynamodb:putItem",
            "ResultPath": null,
            "Parameters": {
              "TableName": "MapStateTable",
              "ReturnConsumedCapacity": "TOTAL",
              "Item": {
                "MessageId": {
                  "S.$": "$.MessageDetails.MessageId"
                },
                "Body": {
                  "S.$": "$.MessageDetails.Body"
                }
              }
            },
            "Next": "Remove message from SQS queue"
          },
          "Remove message from SQS queue": {
            "Type": "Task",
            "Resource": "arn:aws:states:::lambda:invoke",
            "InputPath": "$.MessageDetails",
            "ResultPath": null,
            "Parameters": {
              "FunctionName": "MapStateDeleteFromSQSQueueLambda",
              "Payload": {
                "ReceiptHandle.$": "$.ReceiptHandle"
              }
            },
            "Next": "Publish message to SNS topic"
          },
          "Publish message to SNS topic": {
            "Type": "Task",
            "Resource": "arn:aws:states:::sns:publish",
            "InputPath": "$.MessageDetails",
            "Parameters": {
              "Subject": "Message from Step Functions!",
              "Message.$": "$.Body",
              "TopicArn": "arn:aws:sns:us-east-1:1234567890:MapStateTopicforMessages"
            },
            "End": true
          }
        }
      }
    },
    "Finish": {
      "Type": "Succeed"
    }
  }
}
```

**Dicas para completar**

- Copie/cole este código para substituir a síntaxe do estado `Choice`:

```bash
"Type": "Choice",
"Choices": [
  {
    "Variable": "$",
    "StringEquals": "No messages",
    "Next": "Finish"
  }
```

- Copie/cole este código para substituir a síntaxe do estado `Map`:

```bash
"Type": "Map",
"Next": "Finish",
"ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.Map.Item.Index",
        "MessageDetails.$": "$$.Map.Item.Value"
},
```

5. Definições de ASL podem conter parâmetros de recursos. Atualize o ARN do tópico com o valor correto copiado acima.

6. Clique em **Save** (selecione Save anyway se o alerta aparecer)
   ![save](/static/img/module-5/map-state-definition.png)
