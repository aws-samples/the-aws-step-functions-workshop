---
title: 'Execute the state machine'
weight: 113
---

- Click on **Start execution** and use the below as your input payload.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "Testing AWS SDK integration"
}
:::

- Inspect the **Execution event history** to view a list events and find one called **TaskSucceeded**. Click to expand this event and you should find a list of S3 buckets with one named `univesalsdkintegrationbucket-`.

::alert[**Congratulations!** You have successfully completed an AWS SDK service integration.]{type="success"}
