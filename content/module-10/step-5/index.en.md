---
title: 'Testing the project'
weight: 125
---

After you create your API Gateway REST API with Synchronous Express State Machine as the backend integration, you can test the API Gateway.

### Test the deployed API Gateway using API Gateway console

1. Open the [Amazon API Gateway console](https://console.aws.amazon.com/apigateway/) and sign in.
2. Choose your REST API named, `SAMStepFunctionsRestApi`.
3. In the **Resources** pane, you can select the method you want to test. Click on the `POST` method.
   ![API Gateway POST](/static/img/module-10/api-gateway-testing.png)
4. In the **Method Execution** pane, in the **Client** box, choose **TEST**.
5. Choose **POST** from the **Method Drop-down** menu. Copy/paste the JSON below into the **Request Body** field.
:::code{showCopyAction=true showLineNumbers=true language=json}
{
"key": "Hello Step Functions!"
}
:::
6. Click **Test**. The following information will be displayed:

- **Request** is the resource's path that was called for the method.
- **Status** is the response's HTTP status code.
- **Latency** is the time between the receipt of the request from the caller and the returned response.
- **Response Body** is the HTTP response body.
- **Response Headers** are the HTTP response headers.
- **Logs** are the simulated Amazon CloudWatch Logs entries that would have been written if this method were called outside of the API Gateway console.
  ::alert[Although the CloudWatch Logs entries are simulated, the results of the method call are real.]{header="Note"}

The **Response Body** output should be:

```bash
"Hello back to you!"
```

### Test the deployed API using cURL

- Open a new terminal window in your AWS Cloud9 environment.
- Copy the following cURL command and paste it into the terminal window, replacing `<api-id>` with your API's API ID and `<region>` with the region where your API is deployed. You may have copied this URL in from the CloudFormation output in the last step. You can also find the full invoke URL in the API Gateway console by navigating to **Stages > dev**.

```bash
curl -X POST\
 'https://<api-id>.execute-api.<region>.amazonaws.com/dev' \
 -d '{"key":"Hello Step Functions"}' \
 -H 'Content-Type: application/json'
```

The **Response Body** output should be:

```bash
"Hello back to you!"
```

::alert[**Congratulations!** You have successfully completed this module.]{type="success"}
