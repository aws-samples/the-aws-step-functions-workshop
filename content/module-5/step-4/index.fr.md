---
title: "Localisez vos ressources et configurez votre machine à états"
weight: 74
---

### Localisez vos ressources

Accédez aux services ci-dessous dans la console AWS pour vous familiariser avec les ressources. Assurez-vous d'être dans la bonne région. Copiez l'ARN de la rubrique SNS (Amazon Resource Name) dans un bloc-notes. Vous aurez besoin de cette valeur plus tard dans le module.

- [AWS Lambda](https://console.aws.amazon.com/lambda/home) - trouvez **MapStateReadFromSQSQueueLambda** et **MapStateDeleteFromSQSQueueLambda**

- [Amazon SQS](https://console.aws.amazon.com/sqs/v2/home) - trouvez **MapStateQueueforMessages**

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) - trouvez **MapStateTable**

- [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) - trouvez **MapStateTopicforMessages** *(copiez l'ARN de la rubrique)*

### Configurez votre machine à états

1. Accédez à [Step Functions](https://console.aws.amazon.com/states/home) dans la console AWS.

2. Localisez la machine à états qui contient **MapStateStateMachine** dans son nom. Cliquez dessus, puis cliquez sur **Modifier** dans le coin supérieur droit.

![Modifier la machine à états](/static/img-fr/module-5/map-state-definition-edit.png)

3. Copiez la définition ASL ci-dessous en cliquant sur l'icône carrée dans le coin supérieur droit de l'exemple de code ci-dessous. Remplacez la définition dans votre machine à états par ce code. La définition ci-dessous contient un total de 4 valeurs **BLANK** dans les champs d'état `Map` et `Choice`. Lisez la documentation pour savoir comment mettre à jour ces valeurs **BLANK** avec la syntaxe et les paramètres d'état corrects. (Les conseils pour reussir sont ci-dessous.)

   - En savoir plus sur la syntaxe d'état [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html).

   - En savoir plus sur les [objets contextuels de l'état Map](https://docs.aws.amazon.com/step-functions/latest/dg/input-output-contextobject.html#contextobject-map)

   - En savoir plus sur la syntaxe d'état [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html).

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

**Conseils**

- Copiez/collez ce code pour remplacer la syntaxe d'état `Choice` :

```bash
"Type": "Choice",
"Choices": [
  {
    "Variable": "$",
    "StringEquals": "No messages",
    "Next": "Finish"
  }
```

- Copiez/collez ce code pour remplacer la syntaxe d'état `Map` :

```bash
"Type": "Map",
"Next": "Finish",
"ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.Map.Item.Index",
        "MessageDetails.$": "$$.Map.Item.Value"
},
```

5. Les définitions ASL peuvent contenir des paramètres de ressource. Mettez à jour le `TopicArn` avec la valeur correcte, copiée précédement dans votre bloc-notes.

6. Cliquez sur `Enregistrer` (enregistrez même en cas d'avertissement)
   ![Bouton enregistrer](/static/img-fr/module-5/map-state-definition.png)
