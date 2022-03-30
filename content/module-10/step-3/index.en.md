---
title: 'Locate your resources and configure your state machine'
weight: 103
---

### Locate your resources

Navigate to the services below in the AWS console to familiarize yourself with the resources. Make sure you are in the correct region. Note the SNS Topic ARN (Amazon Resource Name) and Batch job ARN. 



- [AWS Batch](https://console.aws.amazon.com/batch/v2/home) queue - find **BatchJobQueue**

- [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) topic - find **StepFunctionsSample-BatchJobManagementsggakjhskhb-SNSTopic**


### Configure your state machine

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in the AWS console.

2. Locate the state machine that contains **BatchJobNotificationStateMachine** in its name. Click on it and then click on **Edit** in the top right corner.

![EDIT](/static/img/module-10/errorhandlingbatchjob.png)

3. Sample State machine definition would look like this. Browse through this example state machine as well as the one you see on AWS console to see how Step Functions controls AWS Batch and Amazon SNS by connecting to the Amazon Resource Name (ARN) in the Resource field, and by passing Parameters to the service API.

![EDIT](/static/img/module-10/errorhandlingbatchjob1.png)

:::code{showCopyAction=true showLineNumbers=true language=json}

{
  "Comment": "An example of the Amazon States Language for notification on an AWS Batch job completion",
  "StartAt": "Submit Batch Job",
  "TimeoutSeconds": 3600,
  "States": {
    "Submit Batch Job": {
      "Type": "Task",
      "Resource": "arn:aws:states:::batch:submitJob.sync",
      "Parameters": {
        "JobName": "BatchJobNotification",
        "JobQueue": "arn:aws:batch:us-west-2:123456789012:job-queue/BatchJobQueue-123456789abcdef",
        "JobDefinition": "arn:aws:batch:us-west-2:123456789012:job-definition/BatchJobDefinition-123456789abcdef:1"
      },
      "Next": "Notify Success",
      "Retry": [
        {
          "ErrorEquals": [
            "States.ALL"
          ],
          "IntervalSeconds": 30,
          "MaxAttempts": 2,
          "BackoffRate": 1.5
        }
      ],
      "Catch": [
        {
          "ErrorEquals": [ "States.ALL" ],
          "Next": "Notify Failure"
        }
      ]
    },
    "Notify Success": {
      "Type": "Task",
      "Resource": "arn:aws:states:::sns:publish",
      "Parameters": {
        "Message": "Batch job submitted through Step Functions succeeded",
        "TopicArn": "arn:aws:sns:us-west-2:123456789012:StepFunctionsSample-BatchJobManagement12345678-9abc-def0-1234-567890abcdef-SNSTopic-A2B3C4D5E6F7G"
      },
      "End": true
    },
    "Notify Failure": {
      "Type": "Task",
      "Resource": "arn:aws:states:::sns:publish",
      "Parameters": {
        "Message": "Batch job submitted through Step Functions failed",
        "TopicArn": "arn:aws:sns:us-west-2:123456789012:StepFunctionsSample-BatchJobManagement12345678-9abc-def0-1234-567890abcdef-SNSTopic-A2B3C4D5E6F7G"
      },
      "End": true
    }
  }
}
:::

**Error Handling Parameters**

Also, please check out the [error handling parameters](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html) here:

- ErrorEquals (Required)
> A non-empty array of strings that match error names. When a state reports an error, Step Functions scans through the retriers. When the error name appears in this array, it implements the retry policy described in this retrier.

- IntervalSeconds (Optional)
> An integer that represents the number of seconds before the first retry attempt (1 by default). IntervalSeconds has a maximum value of 99999999.

- MaxAttempts (Optional)
> A positive integer that represents the maximum number of retry attempts (3 by default). If the error recurs more times than specified, retries cease and normal error handling resumes. A value of 0 specifies that the error or errors are never retried. MaxAttempts has a maximum value of 99999999.

- BackoffRate (Optional)
> The multiplier by which the retry interval increases during each attempt (2.0 by default).


::::alert{type="success" header="Example Retry Logic"}
This example of a Retry makes 2 retry attempts after waiting for 3 and 4.5 seconds.
:link[Here's the Error Handling Link]{href="https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html" external="true"} in case you missed it earlier.

:::code{showCopyAction=true showLineNumbers=true language=java}

"Retry": [ {
   "ErrorEquals": [ "States.Timeout" ],
   "IntervalSeconds": 3,
   "MaxAttempts": 2,
   "BackoffRate": 1.5
} ]
:::
::::

**IAM Example**

This example AWS Identity and Access Management (IAM) policy generated for you that includes the least privilege necessary to execute the state machine and related resources. We recommend that you include only those permissions that are necessary in your IAM policies.

Example: 'BatchJobNotificationAccessPolicy'

:::code{showCopyAction=true showLineNumbers=true language=json}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "sns:Publish"
            ],
            "Resource": [
                "arn:aws:sns:us-west-2:123456789012:StepFunctionsSample-BatchJobManagement12345678-9abc-def0-1234-567890abcdef-SNSTopic-A2B3C4D5E6F7G"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "batch:SubmitJob",
                "batch:DescribeJobs",
                "batch:TerminateJob"
            ],
            "Resource": "*",
            "Effect": "Allow"
        },
        {
            "Action": [
                "events:PutTargets",
                "events:PutRule",
                "events:DescribeRule"
            ],
            "Resource": [
                "arn:aws:events:us-west-2:123456789012:rule/StepFunctionsGetEventsForBatchJobsRule"
            ],
            "Effect": "Allow"
        }
    ]
}
:::