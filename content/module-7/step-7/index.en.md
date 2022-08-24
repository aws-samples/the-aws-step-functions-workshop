---
title: 'Monitoring Express Workflows'
weight: 97
---

Monitoring Express Workflows requires using different tools than the ones you use for Standard Workflows. Instead of using the Graph Inspector and the Execution Event History widgets as you would with Standard Workflows, with Express Workflows like `ParallelProcessingMachine` you would use CloudWatch for monitoring.

1. Navigate to the Step Functions console and select the `ParallelProcessingMachine`.
2. All execution history is sent to CloudWatch Logs. Use the Monitoring and Logging tabs in the Step Functions console to gain visibility into Express Workflow executions.
3. The Monitoring tab shows six graphs with CloudWatch metrics for Execution Errors, Execution Succeeded, Execution Duration, Billed Duration, Billed Memory, and Executions Started. 
    ![](/static/img/module-7/express-workflows-metrics.png)
4. Navigate to the Logging tab to view recent logs and the logging configuration, with a link to CloudWatch Logs.
    ![](/static/img/module-7/express-workflows-logs.png)
5. Click to view the Cloudwatch log group to see the detailed history there.

::alert[**Congratulations!** You just monitored the executions for your Step Functions Express Workflow.]{type="success"}