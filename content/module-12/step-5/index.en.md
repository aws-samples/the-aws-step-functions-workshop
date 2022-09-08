---
title: 'Debug failed Step Functions executions using AWS X-Ray'
weight: 145
---

You can use AWS X-Ray to visualize the integration of your state machine, identify performance bottlenecks, and troubleshoot requests that resulted in an error. Your state machine sends trace data to X-Ray, and X-Ray processes the data to generate a service map and searchable trace summaries.

With X-Ray enabled for your state machine, you can trace requests as they are executed in Step Functions. This gives you a detailed overview of an entire Step Functions request. You can use an X-Ray service map to view the latency of a request, including any AWS services that are integrated with X-Ray. You can also configure and customize the sampling rules in X-Ray, to control the amount of requests to record.

More details about X-Ray tracing can be found [here](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html)

Let's enable X-Ray tracing on the DetectSentiment State machine.

1. Navigate to [Step Functions console](https://console.aws.amazon.com/states/home). Make sure you are in the correct region.

2. Click **DetectSentimentStateMachine** State machine.

3. In the `DetectSentimentStateMachine` page, click **Edit**.

4. Under `Tracing` in the Edit page, select **Enable X-Ray tracing**.

:::alert{header="Important" type="warning"}
To trace executions with X-Ray, the Step Functions execution role must have X-Ray permissions. You can either let Step Functions create a new role for you with the necessary permissions by selecting "Create new role" under Permissions, or add them manually to your existing role. This has been already done for you.
:::

5. Click **Save** at the top of the page.

X-Ray tracing is now enabled. Next, go to the X-Ray console.

6. In the AWS console,type `X-Ray` in the search bar, click to open the X-Ray console.

Wait for a few minutes until the X-Ray console is loaded with the Service Map. Rfersh the page, if needed.  You will see the following the Service Map for the DetectSentiment State machine. 

   ![Service Map](/static/img/module-12/x-ray-service-map.png)

As per the X-Ray Service Map, Step Functions State Machine interacts with AWS Lambda and Amazon DynamoDB. 
The red legend on the DetectSentimentStateMachine indicates Faults. You will also notice a purple legend on the sentiment-table node, which indicates throttling. Click on the sentiment-table node to investigate this further.

7. Click **sentiment-table** node.

8. On the Service details pane on the right, select **Throttle** and click **View Traces**

   ![View Traces](/static/img/module-12/x-ray-view-traces.png)

9. In the `Traces` page under Trace list, click one of the traces. 

   ![View Traces](/static/img/module-12/x-ray-traces-list.png)

10. In the Trace details page, you will see an error icon on the AWS::StepFunctions::StateMachine segment.

    ![View Traces](/static/img/module-12/x-ray-trace-error.png)

11. Further down in the Trace, there is an error next to Record Transition subsegment. Click on the error icon.

    ![View Traces](/static/img/module-12/x-ray-exception.png)

The error is caused due to DynamoDB provisioned throughput throttling. 	The level of configured provisioned throughput for the table was exceeded. In order to resolve the issue, you can either increase the provisioned write throughput or change the DynamoDB billing mode from provisioned to on-demand.








