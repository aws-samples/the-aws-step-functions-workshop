---
title: 'Handle a failure using Retry'
weight: 123
---

### Locate your resources

Navigate to the services below in the AWS console to familiarize yourself with the deployed resources. Make sure you are in the correct region.

- [AWS Lambda](https://console.aws.amazon.com/lambda/home) functions - find functions starting with **ErrorHandling**. These functions are designed to produce errors. Copy the ARNs of these Lambda functions for later use. 

- [Step Functions](https://console.aws.amazon.com/states/home) state machines - find the state machine starting with **ErrorHandling**

### Configure ASL to implement a Retry with Lambda

In the exercise below, you will create an ASL definition that invokes a Lambda function. The Lambda function is designed to fail. You will implement a `Retry` for this function, setting maximum attempts with an exponential backoff rate between retries.

1. Click on the state machine named **ErrorHandlingStateMachineWithRetry-...** and click on the **Edit** button on the top right corner of the screen.

2. In the `Resource` field, replace the current value with the ARN of the Lambda function in your account named **ErrorHandlingCustomErrorFunction**. When the state machine invokes this function, the function will fail.

   ![Replace Lambda function ARN](/static/img/module-10/error-handling-state-machine-retry.png)


3. Now implement a `Retry`. Copy the code shown below and and paste it beginning on line 8 between the `Resource` node and the `End` node. 

```bash
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
```

4. Review the Error Handling Parameters. These parameters define the behavior of the `Retry`.

- ErrorEquals (Required)

  > A non-empty array of strings that match error names. When a state reports an error, Step Functions scans through the retriers. When the error name appears in this array, it implements the retry policy described in this retrier.

- IntervalSeconds (Optional)

  > An integer that represents the number of seconds before the first retry attempt (1 by default). IntervalSeconds has a maximum value of 99999999.

- MaxAttempts (Optional)

  > A positive integer that represents the maximum number of retry attempts (3 by default). If the error recurs more times than specified, retries cease and normal error handling resumes. A value of 0 specifies that the error or errors are never retried. MaxAttempts has a maximum value of 99999999.

- BackoffRate (Optional)

  > The multiplier by which the retry interval increases during each attempt (2.0 by default).

For more information about error handling parameters, [review the documentation](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html).


5. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.

6. To view your custom error message, select `StartExecution` in the Graph inspector pane and choose the **Exception** tab.
   ![Failure using Retry output](/static/img/module-10/error-handling-custom-error-retry-output.png)

7. Review the **Execution event history** to get more details on the execution.
   ![Failure using Retry event history](/static/img/module-10/error-handling-custom-error-retry-event-history.png)

### Having problems?

Your ASL definition should be similar to the snippet below. Remember to replace the Lambda function ARN.

```bash
{
  "Comment": "A state machine calling an AWS Lambda function with Retry",
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
When you are ready, you may move onto the next page.
