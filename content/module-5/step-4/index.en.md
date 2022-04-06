---
title: 'Execute the state machine and review results'
weight: 73
---

1. **Subscribe to the Amazon SNS topic**

   - Open the [Amazon SNS console](https://console.aws.amazon.com/sns/home).

   - Choose Topics and choose the topic that was created by the Map state sample project.

   - The name will be similar to **MapStateTopicforMessages**.

   - Under Subscriptions, choose Create subscription.

   - The Create subscription page is displayed, listing the Topic ARN for the topic.

   - Under Protocol, choose Email.

   - Under Endpoint, enter an email address to subscribe to the topic.

   - Choose Create subscription.

   - Open the Subscription Confirmation email in the related account and open the Confirm subscription URL.

   - The Subscription confirmed page is displayed.

:::alert{header="Note" type="warning"}
You must confirm via email before the subscription is active.
:::

![SNS](/static/img/module-5/sns-subscription.png)

2. **Add messages to the Amazon SQS queue**

   - Open the [Amazon SQS console](https://console.aws.amazon.com/sqs/home).

   - Choose the queue that was created by the Map state sample project.

   - The name will be similar to **MapStateQueueforMessages**.

   - In the Queue Actions list, select Send a Message.

   - On the Send a Message window, enter a message and choose Send Message.

   - Choose Send Another Message.

   - Continue entering messages until you have several in the Amazon SQS queue.

   - Choose Close.

![SQS](/static/img/module-5/sqs-send-message.png)

3. Click on **Start execution** and copy and paste the JSON below as your input payload.
   :::code{showCopyAction=true showLineNumbers=false language=json}
   { "Comment": "Testing Map & Choice states" }
   :::

4. When an execution is complete, you can select states on the **Visual workflow** and browse the **Input** and **Output** under **Step details**. You can also check the DynamoDB table to see if the messages that you have put into the SQS queue have been successfully inserted.

![DDB](/static/img/module-5/ddb-map-state.png)
