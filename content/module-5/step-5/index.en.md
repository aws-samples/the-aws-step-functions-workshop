---
title: 'Execute the state machine and review results'
weight: 75
---

1. **Subscribe to the Amazon SNS topic (optional)**

   - Open the [Amazon SNS console](https://console.aws.amazon.com/sns/home).

   - Click to view the Topics 
   
   - Click the **MapStateTopicforMessages** Topic

   - Under Subscriptions, choose Create subscription.

   - The Create subscription page is displayed, listing the Topic ARN for the topic.

   - Under Protocol, choose Email.

   - Under Endpoint, enter your email address.

   - Choose Create subscription.

   - Open the Subscription Confirmation sent to your email address and click the `Confirm subscription` link.

:::alert{header="Note" type="warning"}
You must confirm by clicking the emailed link before the subscription is active.
:::

![SNS](/static/img/module-5/sns-subscription.png)

2. **Add messages to the Amazon SQS queue**

   - Open the [Amazon SQS console](https://console.aws.amazon.com/sqs/home).

   - Click the **MapStateQueueforMessages** queue.

   - Click the **Send and receive messages** button.

   - In the Send Message window, enter a message and click **Send Message**.

   - Continue sending messages until you have many in the queue.

   :::alert{header="Note" type="info"}
   With only a few items in the queue, the SQS ReceiveMessage action may sometimes return only a single message. To increase your chances of retrieving and processing multiple messages, add more messages to the queue. 
   :::

![SQS](/static/img/module-5/sqs-send-message.png)

3. Return to [Step Functions](https://console.aws.amazon.com/states/home). Click the **MapStateMachine** and **Start execution**. Copy/paste the JSON below as your input payload.
   :::code{showCopyAction=true showLineNumbers=false language=json}
   { "Comment": "Testing Map & Choice states" }
   :::

4. When an execution is complete, select some of the states on the **Graph Inspector** and view their **Input** and **Output** values. If you created an email subscription you should receive email messages. You may also check [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) table to see if items have been successfully put into the **MapStateTable**.

![DDB](/static/img/module-5/ddb-map-state.png)

::alert[**Congratulations!** You have executed a state machine using the using Map and Choice states.]{type="success"}
