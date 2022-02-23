---
title: 'Update the integration to make the execution synchronous'
weight: 94
---

## Making the integration synchronous

1. Go to the API Gateway console and select the API already created for this activity.
   ![API Console](/static/module-7-API-console-4.png)
2. From the list of resources find the `execution` resource and click on `POST`
   ![API Execution](/static/module-7-API-execution-new-4.png)
3. Click on `Integration Request`
4. Edit the `Action` by clicking the gray pencil and change it to `StartSyncExecution` and click on the update button (gray checkmark)
   ![API Execution Sync](/static/module-7-API-integration-setup-sync.png)
5. Test your API again.
6. You will notice a larger `Response Body` with more details from the state machine execution including the `input` and the `output`
   ![API Test Result Sync](/static/module-7-API-test-result-sync-4.png)

Congratulations! You just setup a synchronous integration between API Gateway and Step Functions without writing a single line of code.
