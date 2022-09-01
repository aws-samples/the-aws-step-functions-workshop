---
title: 'Logging Step Functions to CloudWatch'
weight: 143
---

Standard Workflows record execution history in AWS Step Functions, although you can optionally configure logging to Amazon CloudWatch Logs. When you create a Standard Workflow, it will not be configured to enable logging to CloudWatch Logs. To configure logging, you can pass the LoggingConfiguration parameter when using CreateStateMachine or UpdateStateMachine. You can further analyze your data in CloudWatch Logs by using CloudWatch Logs Insights. For more information see [Analyzing Log Data with CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html).

Also read the [required IAM policies](https://docs.aws.amazon.com/step-functions/latest/dg/cw-logs.html#cloudwatch-iam-policy) for logging to CloudWatch Logs.

1. Open the [Step Functions Console](https://console.aws.amazon.com/states/home) in your AWS console. Make sure you are in the correct region.

2. Click **State machines** on the left navigation and you will see the State machine - DetectSentimentMachine deployed for you as part of this lab.

3. Click DetectSentimentMachine State machine. 

4. In the DetectSentimentMachine page, click **Logging** tab. You will see the Log level is OFF which indicates logging is not enabled. 

   ![CW Log disabled](/static/img/module-12/cw-log-disabled.png)

    Let's enable CW Logging.

5. Click **Edit** at the top of the page.

6. In the Edit DetectSentimentStateMachine page, update the **Logging** to **ALL** and keep the rest as default.

   ![CW Log enabled](/static/img/module-12/cw-logging-enabled.png)

7. Click **Save** at the top of the page.

8. In the IAM role dialog box, click **Save anyway**.

Wait for a few minutes. Refresh the page and you will see the CloudWatch Logs Insights section populated with logs.

   ![CW Logs](/static/img/module-12/cw-logs.png)

Alternatively you can click open the CloudWatch Log group link to open the logs in the CloudWatch console.