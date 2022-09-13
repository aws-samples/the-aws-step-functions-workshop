---
title: 'Debug failed executions with AWS X-Ray Traces'
weight: 145
---

You can use AWS X-Ray to visualize the integrations in your state machine, to identify performance bottlenecks, and to troubleshoot failed requests. When your state machine sends trace data to X-Ray, X-Ray processes the data to generate a service map and searchable trace summaries.

With X-Ray enabled for your state machine, you can trace the paths of your requests giving you a detailed visual overview of your entire workflow. You can use X-Ray service maps to view request latency, including any AWS services that are integrated with X-Ray. You can also configure and customize the sampling rules in X-Ray to control the frequency of recorded requests.

To learn more read [AWS X-Ray and Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html).

## Enable X-Ray tracing on DetectSentimentStateMachine.

1. Navigate to [Step Functions console](https://console.aws.amazon.com/states/home). Make sure you are in the correct region.

2. Click **DetectSentimentStateMachine** State machine.

3. In the `DetectSentimentStateMachine` page, click **Edit**.

4. Under `Tracing` in the Edit page, select **Enable X-Ray tracing**.

:::alert{header="Important" type="warning"}
To trace executions with X-Ray, the Step Functions execution role must have X-Ray permissions. You can either let Step Functions create a new role for you with the necessary permissions by selecting "Create new role" under Permissions, or add them manually to your existing role. This has been already done for you.
:::

5. Click **Save** at the top of the page.

6. Navigate to [X-Ray](https://console.aws.amazon.com/xray/home) in the AWS console.

Wait for a few minutes until the X-Ray console is loaded with the Service Map. Refresh the page, if needed.  You will see the following the Service Map for the DetectSentimentStateMachine. 

   ![Service Map](/static/img/module-12/x-ray-service-map.png)

This Service Map shows that your state machine interacts with AWS Lambda and Amazon DynamoDB. The red legend on the DetectSentimentStateMachine indicates Faults. The purple legend on the sentiment-table node indicates throttling.

7. Click **sentiment-table** node to investigate this throttling.

8. On the Service details pane on the right, select **Throttle** and click **View Traces**

   ![View Traces](/static/img/module-12/x-ray-view-traces.png)

9. In the `Traces` page under Trace list, click one of the traces. 

   ![View Traces](/static/img/module-12/x-ray-traces-list.png)

10. In the Trace details page, you will see an error icon on the AWS::StepFunctions::StateMachine segment.

    ![View Traces](/static/img/module-12/x-ray-trace-error.png)

11. Further down in the Trace, there is an error next to Record Transition subsegment. Click on the error icon.

    ![View Traces](/static/img/module-12/x-ray-exception.png)

The error is caused by DynamoDB provisioned throughput throttling. The requested throughput exceeded the configured level of provisioned capacity. To resolve the issue, you can reduce your requested throughput by decreasing the frequency of your writes, or you can increase your capacity by increasing your provisioned write capacity units or by changing the DynamoDB billing mode from provisioned to on-demand.








