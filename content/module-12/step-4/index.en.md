---
title: 'Record execution history with Amazon CloudWatch Logs'
weight: 144
---

Standard Workflows record execution history in AWS Step Functions, although you can optionally configure logging to Amazon CloudWatch Logs. When you create a Standard Workflow, it will not be configured to enable logging to CloudWatch Logs by default. To configure logging, you can pass the LoggingConfiguration parameter when using CreateStateMachine or UpdateStateMachine. CloudWatch Logs provides several advantages to log files analysis over the default logging, including the capability to further analyze your data by using CloudWatch Logs Insights. For more information see [Analyzing Log Data with CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html). To understand the required IAM policies for logging to CloudWatch Logs read [IAM Policies for logging to CloudWatch Logs](https://docs.aws.amazon.com/step-functions/latest/dg/cw-logs.html#cloudwatch-iam-policy).

## Configure CloudWatch Logs

1. Open the [Step Functions Console](https://console.aws.amazon.com/states/home) in your AWS console. Make sure you are in the correct region.

2. Click **State machines** on the left navigation. You will see the State machine named DetectSentimentStateMachine-XXXX deployed for you as part of this lab.

3. Click **DetectSentimentStateMachine-XXXX** State machine. 

4. In the DetectSentimentStateMachine page, click **Logging** tab. You will see the Log level is OFF which indicates CloudWatch logging is not enabled. 

   ![CW Log disabled](/static/img/module-12/cw-log-disabled.png)

    Let's enable CloudWatch logging.

5. Click **Edit** at the top of the page.

6. In the Edit DetectSentimentStateMachine page, scroll down to change the Log level under Logging to **ALL** and leave the rest as default.

   ![CW Log enabled](/static/img/module-12/cw-logging-enabled.png)

7. Click **Save** at the top of the page.

8. In the IAM role dialog box, click **Save anyway**.

Go back to the DetectSentimentStateMachine page and wait for a few minutes. Refresh the page and you will see the CloudWatch Logs Insights section populated with logs.

   ![CW Logs](/static/img/module-12/cw-logs.png)

## Query CloudWatch Logs Insights

1. Open the [CloudWatch console](https://console.aws.amazon.com/cloudwatch/home). Click **Logs Insights** under Logs on the left navigation menu.

2. In the Logs Insights page, select **/aws/vendedlogs/states/DetectSentimentStateMachine-XXX-Logs** log group.

   ![CWL Vended](/static/img/module-12/cwl-vendedlogs.png)

3. In the text field, copy paste the following query and click **Run query**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, type
| stats count(*) as typeCount by type 
| sort typeCount desc
:::

This CloudWatch Log Insights query displays the stats of various execution types.

   ![CWL query](/static/img/module-12/cwl-query.png)

   Scroll down in the result section to review the complete results. You will see TaskFailed and ExecutionFailed results.

   ![CWL failed](/static/img/module-12/cwl-failed.png)

12. To identify the cause of the failed executions, copy and paste the following query in the CloudWatch Log Insights text field and click **Run query**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, execution_arn, details.error, details.cause
| filter type = 'TaskFailed'
| limit 100
:::

![CWL failureReasons 1](/static/img/module-12/cwl-failureReasons-1.png)

![CWL CWL failureReasons 2](/static/img/module-12/cwl-failureReasons-2.png)

These errors indicate Step Functions execution failures were due to the DynamoDB provisioned throughput throttling. In the next module, you will use the X-Ray tracing to further investigate these failures.
