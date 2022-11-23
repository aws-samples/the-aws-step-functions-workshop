---
title: 'Locate your resources and configure your state machine'
weight: 74
---

### Locate your resources

Navigate to the services below in the AWS console to familiarize yourself with the resources. Make sure you are in the correct region. Copy the SNS Topic ARN (Amazon Resource Name) to a notepad. You will need this value later in the module.

- [AWS Lambda](https://console.aws.amazon.com/lambda/home) - find **MapStateReadFromSQSQueueLambda** and **MapStateDeleteFromSQSQueueLambda**

- [Amazon SQS](https://console.aws.amazon.com/sqs/v2/home) - find **MapStateQueueforMessages**

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) - find **MapStateTable**

- [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) - find **MapStateTopicforMessages** *(copy the Topic ARN)*

### Configure your state machine

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in the AWS console.

2. Locate the state machine that contains **MapStateStateMachine** in its name. Click on it and then click on **Edit** in the top right corner.

![EDIT](/static/img/module-5/map-state-definition-edit.png)

3. Copy the ASL definition below by clicking the square icon in the top right corner of the code sample field. Replace the definition in your state machine with this copied code. This definition below contains a total of 4 **BLANK** values in the Map and Choice state fields. Read the documentation to learn how to the update these **BLANK** values with the correct state syntax and parameters. (Completion hints are below.)

   - Learn about [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) state syntax.

   - Learn about [Map State context objects](https://docs.aws.amazon.com/step-functions/latest/dg/input-output-contextobject.html#contextobject-map)
   
   - Learn about [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) state syntax.

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

**Completion Hints**

- Copy/paste this code to replace the `Choice` state syntax:

```bash
"Type": "Choice",
"Choices": [
  {
    "Variable": "$",
    "StringEquals": "No messages",
    "Next": "Finish"
  }
```

- Copy/paste this code to replace the `Map` state syntax:

```bash
"Type": "Map",
"Next": "Finish",
"ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.Map.Item.Index",
        "MessageDetails.$": "$$.Map.Item.Value"
},
```

5. ASL definitions may contain resource parameters. Update the TopicArn with the correct value, copied from above.

6. Click on **Save** (select Save anyway if the warning comes)
   ![save](/static/img/module-5/map-state-definition.png)
