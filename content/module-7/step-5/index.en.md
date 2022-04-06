---
title: 'Execute a synchronous execution through API Gateway'
weight: 95
---

## Make the integration synchronous

1. Go to the API Gateway console and select the API created for this module.
   ![API Console](/static/img/module-7/api-console-4.png)
2. From the list of resources find the `execution` resource and click on `POST`
   ![API Execution](/static/img/module-7/api-execution-new-4.png)
3. Click on `Integration Request`
4. Edit the `Action` by clicking the gray pencil and change it to `StartSyncExecution` and click on the update button (gray checkmark)
   ![API Execution Sync](/static/img/module-7/api-integration-setup-sync.png)
5. Test your API again.
6. You will notice a larger `Response Body` with more details from the state machine execution including the `input` and the `output`
   ![API Test Result Sync](/static/img/module-7/api-test-result-sync-4.png)

::alert[**Congratulations!** You just executed a synchronous integration between API Gateway and Step Functions.]{type="success"}
