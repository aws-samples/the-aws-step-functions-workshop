---
title: 'Execute the state machine through API Gateway and review results'
weight: 94
---

1. Go to the API Gateway console and select the API already created for this activity.
   ![API Console](/static/img/module-7/module-7-API-console-3.png)
2. From the list of resources find the `execution` resource and click on `POST`
   ![API Execution New](/static/img/module-7/module-7-API-execution-new.png)
3. Click on `Test`
4. At the bottom of the page you will find a field called `Request Body`, paste the following json there and replace the sample `stateMachineArn` with the ARN of your State Machine.
   :::code{showCopyAction=true language=json}
   {
   "input": "{\"data\": [20,40,60,10,9]}",
   "name": "MyExecution",
   "stateMachineArn": "arn:aws:states:us-east-1:123456789012:stateMachine:ParallelProcessing-sm"
   }
   :::
   ![API Test](/static/img/module-7/module-7-API-test.png)
5. Click `Test`
6. Look at the `Response Body`, you can notice that it includes the reference to the `executionArn` and the `startDate`, this is because the State Machine was executed asynchronously
   ![API Test Result](/static/img/module-7/module-7-API-test-result.png)

   In the next section, let's change the configuration to make it synchronous.
