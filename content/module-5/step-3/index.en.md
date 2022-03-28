---
title: 'Locate your resources and configure your state machine'
weight: 72
---

### Locate your resources

Navigate to the services below in the AWS console to familiarize yourself with the resources. Make sure you are in the correct region. Copy the SNS Topic ARN (Amazon Resource Name) to a notepad. You will need this value later in the module. 

- [Amazon SQS](https://console.aws.amazon.com/sqs/v2/home) queue - find **MapStateQueueforMessages**

- [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) topic - find **MapStateTopicforMessages**

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) table - find **MapStateTable**

- [AWS Lambda](https://console.aws.amazon.com/lambda/home) functions - find **MapStateReadFromSQSQueueLambda** and **MapStateDeleteFromSQSQueueLambda**

### Configure your state machine

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in the AWS console.

2. Locate the state machine that contains **MapStateStateMachine** in its name. Click on it and then click on **Edit** in the top right corner.

![EDIT](/static/img/module-5/extra-credit-map-state-definition-edit.png)

3. Select all under the **Definition** section and delete the existing ASL definition. Now copy and paste the ASL definition below. This definition contains **BLANK** values in the Map and Choice state (total of 4 places). Your challenge is to update these **BLANKs** with the correct state syntax and parameters. (Completion hints are below.)

    - Visit [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) to learn about Map state syntax.

    - Visit [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) to learn about Choice state syntax.

:::code{showCopyAction=true showLineNumbers=true language=json}

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
:::

**HINTS**


- Choice State Syntax:

:::code{showCopyAction=true showLineNumbers=true language=json}

"Type": "Choice",
"Choices": [
{
"Variable": "$",
"StringEquals": "No messages",
"Next": "Finish"
}
:::

- Map State Syntax:

:::code{showCopyAction=true showLineNumbers=true language=json}

"Type": "Map",
"Next": "Finish",
"ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.Map.Item.Index",
        "MessageDetails.$": "$$.Map.Item.Value"
}
:::

5. ASL definitions may contain resource parameters. Find and update the TopicArn with the correct value.

6. Click on **Save** (select Save anyway if the warning comes)
   ![save](/static/img/module-5/extra-credit-map-state-definition.png)
   
