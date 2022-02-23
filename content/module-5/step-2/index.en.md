---
title: 'Create the state machine and provision resources'
weight: 72
---

The following resources are already created for you in your AWS account. Navigate to these services on the AWS console to grab the required resource names and ARNs (Amazon Resource Name) which will be needed in the later steps of this exercise. It is recommended that you copy these values in a notepad.

- An Amazon SQS queue - will be similar to `MapStateQueueforMessages`

- An Amazon SNS topic - will be similar to `MapStateTopicforMessages`

- A DynamoDB table - will be similar to `MapStateTable`

- Two Lambda functions - will be similar to `MapStateReadFromSQSQueueLambda` and `MapStateDeleteFromSQSQueueLambda`

1. Navigate to Step Functions in your AWS console. Make sure you are in the same AWS region that is assigned for this session.

2. If you are not on the State Machines page, click on State Machines on the left side menu and you will see a state machine that will look like **MapStateStateMachine-tshNzXAbA3tM**. Click on it and then click on **Edit** from the right top corner.

![EDIT](/static/extra-credit-map-state-definition-edit.png)

3. Select all under the **Definition** section and delete the existing **Definition** which is a hello world state definition. Now copy and paste the state machine definition from below which has **BLANK** values in the Map and Choice state (total of 4 places). Please make sure you update these **BLANKs** with the correct state syntax and parameters.

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

Visit [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) to explore Map state syntax.

Visit [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) to explore Choice state syntax.

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

Map State Syntax:

:::code{showCopyAction=true showLineNumbers=true language=json}

"Type": "Map",
"Next": "Finish",
"ItemsPath": "$",
      "Parameters": {
        "MessageNumber.$": "$$.Map.Item.Index",
        "MessageDetails.$": "$$.Map.Item.Value"
}
:::

5. State machine definition may also have the sample resource parameters. Cross check and update the state machine definition parameters/resources with the resource names/ARNs noted in step 1. Make sure SNS topic ARN has your correct AWS account number.

6. Click on **Save** (select Save anyway if the warning comes)
   ![save](/static/extra-credit-map-state-definition.png)
