---
title: 'Trying out different error scenarios'
weight: 123
---

### Locate your resources

Navigate to the services below in the AWS console to familiarize yourself with the resources already setup for you. Make sure you are in the correct region. Note the Lambda Function ARN (Amazon Resource Name) and Step Function ARN.

- [AWS Lambda](https://console.aws.amazon.com/lambda/home) functions - find functions starting with **ErrorHandling**

- [Step Functions](https://console.aws.amazon.com/states/home) state machines - find state machine starting with **ErrorHandling**

### Handling a failure using Catch

1. Copy the **Function ARN** of the Lambda function named **ErrorHandlingCustomErrorFunction**.

2. Click on the state machine and then click on **Edit** button on the top right corner of the screen. Replace the value of `Resource` with the Lambda ARN copied in the previous step as shown in the diagram below.
   ![Custom Lambda ARN](/static/img/module-10/error-handling-custom-lambda-arn.png)

3. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.

4. Go to the **Execution output** tab to view the output of your workflow. It should show `This is a fallback from a custom Lambda function exception`

5. To view your custom error message, select `StartExecution` in the Graph inspector pane and choose the **Step output** tab
   ![Failure using Catch output](/static/img/module-10/error-handling-custom-error-catch-output.png)
6. Go through the **Execution event history** to get more details
   ![Failure using Catch event history](/static/img/module-10/error-handling-custom-error-catch-event-history.png)

### Handling a failure using Retry

We will now change the state machine definition to include a `Retry` field to retry a function that fails and outputs the error name `CustomError`. The function is retried twice with an exponential backoff between retries.

1. Copy the code shown below and replace the definition of the state machine using the copied version. Replace the value of `Resource` with the Lambda ARN copied earlier.

```bash
{
  "Comment": "A Catch example of the Amazon States Language using an AWS Lambda function",
  "StartAt": "StartExecution",
  "States": {
    "StartExecution": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:FailFunction",
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "End": true
    }
  }
}
```

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

2. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.
3. To view your custom error message, select `StartExecution` in the Graph inspector pane and choose the **Exception** tab
   ![Failure using Retry output](/static/img/module-10/error-handling-custom-error-retry-output.png)
4. Go through the **Execution event history** to get more details
   ![Failure using Retry event history](/static/img/module-10/error-handling-custom-error-retry-event-history.png)

### Handling a timeout using Catch

1. Copy the **Function ARN** of the Lambda function named **ErrorHandlingSleep10Function**.
2. Copy the code shown below and replace the definition of the state machine using the copied version. Replace the value of `Resource` with the Lambda Function ARN copied earlier.

```bash
{
  "Comment": "A Catch example of the Amazon States Language using an AWS Lambda function",
  "StartAt": "StartExecution",
  "States": {
    "StartExecution": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:FailFunction",
      "TimeoutSeconds": 2,
      "Catch": [ {
        "ErrorEquals": ["States.Timeout"],
        "Next": "TimeoutErrorFallback"
      }, {
        "ErrorEquals": ["States.TaskFailed"],
        "Next": "ReservedTypeFallback"
      }, {
        "ErrorEquals": ["States.ALL"],
        "Next": "CatchAllFallback"
      } ],
      "End": true
    },
    "TimeoutErrorFallback": {
      "Type": "Pass",
      "Result": "This is a fallback from a timeout Lambda function exception",
      "End": true
    },
    "ReservedTypeFallback": {
      "Type": "Pass",
      "Result": "This is a fallback from a reserved error code",
      "End": true
    },
    "CatchAllFallback": {
      "Type": "Pass",
      "Result": "This is a fallback from any error code",
      "End": true
    }
  }
}
```

3. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.

4. Go to the **Execution output** tab to view the output of your workflow. It should show `This is a fallback from a timeout Lambda function exception`

5. To view the error message, select `StartExecution` in the Graph inspector pane and choose the **Step output** tab
   ![Failure using Catch output](/static/img/module-10/error-handling-timeout-error-catch-output.png)
6. Go through the **Execution event history** to get more details
   ![Failure using Catch event history](/static/img/module-10/error-handling-timeout-error-catch-event-history.png)

### Handling a timeout using Retry

We will now change the state machine definition to include a `Retry` field to retry a function that times out. The function is retried twice with an exponential backoff between retries.

1. Copy the code shown below and replace the definition of the state machine using the copied version. Replace the value of `Resource` with the Lambda ARN copied earlier.

```bash
{
  "Comment": "A Catch example of the Amazon States Language using an AWS Lambda function",
  "StartAt": "StartExecution",
  "States": {
    "StartExecution": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:FailFunction",
      "TimeoutSeconds": 2,
      "Retry": [
        {
          "ErrorEquals": [
            "States.Timeout"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "End": true
    }
  }
}
```

2. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.
3. To view your custom error message, select `StartExecution` in the Graph inspector pane and choose the **Exception** tab
   ![Failure using Retry output](/static/img/module-10/error-handling-timeout-error-retry-output.png)
4. Go through the **Execution event history** to get more details
   ![Failure using Retry event history](/static/img/module-10/error-handling-timeout-error-retry-event-history.png)

   ::alert[Congratulations! You have successfully completed the module.]{type="success"}
