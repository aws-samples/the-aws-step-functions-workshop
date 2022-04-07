---
title: 'Testing the project'
weight: 113
---

After you create your API Gateway REST API with Synchronous Express State Machine as the backend integration, you can test the API Gateway.

::alert[For the purpose of this tutorial, we will test the `POST` HTTP method.]{header="Note"}

### To test the deployed API Gateway using API Gateway console

1. Open the [Amazon API Gateway console](https://console.aws.amazon.com/apigateway/) and sign in.
2. Choose your REST API named, `StepFunctionsRestApi`.
3. In the **Resources** pane, choose the method you want to test. For the purpose of this tutorial, this will be the `ANY` method.
   ![API GAteway ANY](/static/img/module-9/api-gateway-testing.png)
4. In the **Method Execution** pane, in the **Client** box, choose **TEST**.
5. Choose **POST** from the **Method Drop-down** menu. Type values in the **Request Body**. The console includes these values in the method request in default application/json form. For the purpose of this tutorial type the following into the **Request Body**:
   :::code{showCopyAction=true showLineNumbers=true language=json}
   {
   "key": "Hello"
   }
   :::
6. Choose **Test**. The following information will be displayed:

- **Request** is the resource's path that was called for the method.
- **Status** is the response's HTTP status code.
- **Latency** is the time between the receipt of the request from the caller and the returned response.
- **Response Body** is the HTTP response body.
- **Response Headers** are the HTTP response headers.
- **Logs** are the simulated Amazon CloudWatch Logs entries that would have been written if this method were called outside of the API Gateway console.
  ::alert[Although the CloudWatch Logs entries are simulated, the results of the method call are real.]{header="Note"}

The **Response Body** output should be something like this:

```bash
"Hello"
```

### To test the deployed API using cURL

- Open a new terminal window in your Cloud9 environment.
- Copy the following cURL command and paste it into the terminal window, replacing `<api-id>` with your API's API ID and `<region>` with the region where your API is deployed.

```bash
curl -X POST\
 'https://<api-id>.execute-api.<region>.amazonaws.com/prod' \
 -d '{"key":"Hello"}' \
 -H 'Content-Type: application/json'
```

The **Response Body** output should be something like this:

```bash
"Hello"
```

::alert[**Congratulations!** You have successfully completed this module.]{type="success"}