---
title: 'Fix the errors and check the X-Ray traces'
weight: 145
---

1. Navigate to [DynamoDB console](https://console.aws.amazon.com/dynamodbv2/home). Make sure you are in the correct region.

2. Click **Tables** in the left menu.

3. Click the **sentiment-table** in the center pane.

4. Under Additional settings, click **Edit**.

5. In the Edit read/write capacity page, select **On-demand Capacity** mode and click **Save** changes.

   ![Update DDB](/static/img/module-12/ddb-update-table.png)

Changing from Provisioned to On-demand will take a few minutes. You can check the Table Status under Overview table and wait until its updated to Active.
   
   ![Updated DDB](/static/img/module-12/ddb-on-demand.png)

Next, go to X-Ray console to verify if there are any more throttles.

6. In the AWS console,type `X-Ray` in the search bar, click to open the X-Ray console.

7. In the center, update the timeframe to 1 min.

   ![No throttles](/static/img/module-12/x-ray-update-time.png)

You will now notice that there are no more faults or throttles. 

   ![No throttles](/static/img/module-12/x-ray-no-throttles.png)

If you check the CloudWatch metrics for the Step Functions execution, you will see that the ExecutionsFailed has dropped to 0. 

   ![Zero Failed executions](/static/img/module-12/cw-states-execution-metrics-0.png)

   ::alert[Congratulations! You have successfully completed the Error Handling module.]{type="success"}
