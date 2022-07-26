---
title: 'Handle a failure using Catch'
weight: 123
---

`Task`, `Map`, and `Parallel` states may contain a field named `Catch`. This field's value must be an array of objects, known as catchers. Each catcher can be configured to catch a specific type of error. ASL defines a set of built-in strings that name well-known errors, all beginning with the `States.` prefix. Catchers may also catch custom errors. Each catcher may be configured to forward to a specific **fallback** state. Each fallback state may implement error handling logic. Built-in error types include:

- `States.ALL` - a wildcard that matches any known error name
- `States.DataLimitExceeded` - an output exceeds quota
- `States.Runtime` - a runtime exception could not be processed
- `States.HeartbeatTimeout` - a Task state failed to send a heartbeat
- `States.Timeout` - a Task state timed out
- `States.TaskFailed` - a Task state failed during execution
- `States.Permissions` - a Task state had insufficient privileges

When a state has both Retry and Catch fields, Step Functions uses any appropriate retriers first, and only afterward applies the matching catcher transition if the retry policy fails to resolve the error.

Read the documentation for more information on [Error names](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html).

In this exercise, you will configure a state machine that will catch a custom error and a `States.Timeout` error using the `Catch` field. 

### Catch a custom error

1. Locate the **ErrorHandlingCustomErrorFunction** [Lambda function](https://console.aws.amazon.com/lambda/home). Copy the function ARN and review the code. Notice that the code throws an error named `CustomError`.

   ![Lambda function throws CustomError](/static/img/module-11/error-handling-lambda-function-custom-error.png)

2. Now locate the **ErrorHandlingStateMachineWithCatch-...** [state machine](https://console.aws.amazon.com/states/home). Click on its link and click the **Edit** button on the top right corner of the screen. 

3. In the `Resource` field, replace the current value with the ARN of the Lambda function copied in step 1. When the state machine invokes this function, the function will fail with the `CustomError`.

   ![Replace Lambda function ARN](/static/img/module-11/error-handling-state-machine-catch.png)

4. Review the `Catch` block of your ASL definition. Notice that it contains three catchers. The first catcher is configured to catch an error called `CustomError`. When it catches this error it passes flow control to the fallback state `CustomErrorFallback`.

   ![Catch CustomError](/static/img/module-11/error-handling-state-machine-catch-custom-error.png)

5. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.

6. Go to the **Execution output** tab to view the output of your workflow. It should show `This is a fallback from a custom Lambda function exception`

7. To view the output of the fallback state, select `CustomErrorFallback` state in the Graph inspector pane and click the **Step output** tab.
   ![Failure using Catch output](/static/img/module-11/error-handling-custom-error-catch-output.png)
8. Go to the **Execution event history** to get more details.
   ![Failure using Catch event history](/static/img/module-11/error-handling-custom-error-catch-event-history.png)



### Catch a timeout error

1. Locate the **ErrorHandlingSleep10Function** [Lambda function](https://console.aws.amazon.com/lambda/home). Copy the function ARN and review the code. Notice that the function is configured to sleep for 10 seconds.

   ![Lambda function sleeps for 10 seconds](/static/img/module-11/error-handling-lambda-sleep10.png)

2. Now locate the **ErrorHandlingStateMachineWithCatch-...** [state machine](https://console.aws.amazon.com/states/home). Click on its link and click the **Edit** button on the top right corner of the screen. 

3. In the `Resource` field, replace the current value with the ARN of the Lambda function copied in step 1. When the state machine invokes this function, the function will sleep for 10 seconds.

   ![Replace Lambda function ARN](/static/img/module-11/error-handling-state-machine-catch.png)

4. Notice the `TimeoutSeconds` field for the `Task` is set to be 5 seconds. Notice the catcher configured to catch the `States.Timeout` error type. This catcher forwards to the `TimeoutFallback` state. 

   ![Review the Timeout Catcher](/static/img/module-11/error-handling-state-machine-timeout.png)

5. Click **Save** and then **Start execution**. Accept the default input and click **Start execution** again.

6. Go to the **Execution output** tab to view the output of your workflow. It should show `This is a fallback from a timeout Lambda function exception`

7. To view the output of the fallback state, select `TimeoutFallback` state in the Graph inspector pane and click the **Step output** tab.
   ![Failure using Catch output](/static/img/module-11/error-handling-timeout-error-catch-output.png)

8. Go through the **Execution event history** to get more details
   ![Failure using Catch event history](/static/img/module-11/error-handling-timeout-error-catch-event-history.png)

   ::alert[Congratulations! You have successfully completed the Error Handling module.]{type="success"}
