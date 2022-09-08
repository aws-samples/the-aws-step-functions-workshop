---
title: 'Monitor Step Functions executions with Amazon CloudWatch Metrics'
weight: 143

---

Monitoring is an important part of maintaining the reliability, availability, and performance of AWS Step Functions and your AWS solutions. 

The CloudFormation Stack that you launched in the previous step has deployed DetectSentimentStateMachine Step Functions and few other resources.

   ![DetectSentiment State Machine](/static/img/module-12/state-machine.png)

This state machine takes an input string, detects sentiment of this text and records the transaction in DyanmoDB. This state machine is triggered at frequent intervals. 

In this exercise, you will use CloudWatch metric to monitor the DetectSentimentStateMachine Step Functions executions.

The following Step Functions Execution metrics are available in CloudWatch 
- ExecutionTime	
- ExecutionThrottled
- ExecutionsAborted	
- ExecutionsFailed	
- ExecutionsStarted	
- ExecutionsSucceeded	
- ExecutionsTimedOut

More details about these metrics can be found [here](https://docs.aws.amazon.com/step-functions/latest/dg/procedure-cw-metrics.html#cloudwatch-step-functions-execution-metrics)

1. Navigate to [CloudWatch Console](https://console.aws.amazon.com/cloudwatch/home) in your AWS console. Make sure you are in the correct region.

2. Under `Metrics` on the left navigation menu, click **All Metrics**. In the center, under `Metrics`, select **States**.

   ![CW All Metrics States](/static/img/module-12/cw-all-metrics-states.png)

3. Click **Execution Metrics** under `States` metrics.

   ![Execution Metrics](/static/img/module-12/cw-states-execution-metrics.png)

4. Select all the metrics listed for `DetectSentimentStateMachine`. 

   ![DetectSentiment Metrics](/static/img/module-12/cw-detect-sentiment-metrics.png)

5. Click the **Graphed metrics** tab. Update the `Statistic` column of `ExecutionTime` to **Average** and the `Statistic` for rest of the metrics to **Sum**. On the top right change the legend from Line to `Number`.

   ![Sum and Average](/static/img/module-12/cw-metrics-sum-avg.png)

6. Click the edit pencil next to the graph title, and enter **Execution Metrics**. 

7. In the top right, click the **Actions** dropdown and choose **Add to dashboard**.

-  In the **Add to dashboard** page, click **Create new**.
- Enter *DetectSentiment* for the dashboard name and click **Create**.
- For **widget type**, select Number.
- Click **Add to dashboard**.

   ![CW Metrics](/static/img/module-12/cw-add-dashboard.png)

8. Choose **Save dashboard**.

You can now see the execution metrics for DetectSentiment State Machine Step Functions. You will notice there are a few executions that have failed, indicated by ExecutionsFailed metrics.

   ![Dashboard Metrics](/static/img/module-12/cw-dashboard.png)

In the next modules, you will use CloudWatch Logs and X-Ray tracing to debug and identify the root cause of these failures.