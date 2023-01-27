---
title: 'Localiza los recursos y configura la máquina de estado'
weight: 74
---

### Localiza los recursos

Navega hasta los siguientes servicios en la consola de AWS para familiarizarse con los recursos. Asegúrate de estar en la región correcta. Copia el ARN del tema de SNS (nombre de recurso de Amazon) en un bloc de notas. Necesitará este valor más adelante en el módulo.


- [AWS Lambda](https://console.aws.amazon.com/lambda/home) - busca **MapStateReadFromSQSQueueLambda** y **MapStateDeleteFromSQSQueueLambda**

- [Amazon SQS](https://console.aws.amazon.com/sqs/v2/home) - busca **MapStateQueueforMessages**

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) - busca **MapStateTable**

- [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) - busca **MapStateTopicforMessages** *(copia el ARN del tema)*

### Configura tu máquina de estado

1. Ve a [Step Functions](https://console.aws.amazon.com/states/home) en la consola de AWS.

2. Busca la máquina de estado que contiene **MapStateStateMachine** en su nombre. Haz clic en él y, a continuación, en **Edit** en la esquina superior derecha.

![EDIT](/static/img/module-5/map-state-definition-edit.png)

3. Copia la definición de ASL que aparece a continuación haciendo clic en el icono cuadrado de la esquina superior derecha del campo de ejemplo de código. Sustituya la definición en su máquina de estado por este código copiado. La siguiente definición contiene un total de 4 valores **BLANK** en los campos de estado `Map` y `Choice`. Lea la documentación para obtener información sobre cómo actualizar estos valores **BLANK** con la sintaxis de estado y los parámetros correctos. (Las sugerencias de finalización se encuentran a continuación).

 - Obtenga información sobre la sintaxis de estados de [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html).

 - Más información sobre [el objeto `context` para estados Map](https://docs.aws.amazon.com/step-functions/latest/dg/input-output-contextobject.html#contextobject-map)
 
 - Obtenga información sobre la sintaxis de estados de [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html).

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

**Sugerencias para completar**

- Copia y pega este código para reemplazar la sintaxis del estado `Choice`:

```bash
"Type": "Choice",
"Choices": [
  {
    "Variable": "$",
    "StringEquals": "No messages",
    "Next": "Finish"
  }
]
```

- Copia y pega este código para reemplazar la sintaxis del estado `Map`:

```bash
"Type": "Map",
"Next": "Finish",
"ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.Map.Item.Index",
        "MessageDetails.$": "$$.Map.Item.Value"
},
```

5. Las definiciones de ASL pueden contener parámetros de recursos. Actualiza el `TopicArn` con el valor correcto, copiado de arriba.

6. Haz clic en **Save** (selecciona Guardar de todos modos si aparece la advertencia)
    ![save](/static/img/module-5/map-state-definition.png)
