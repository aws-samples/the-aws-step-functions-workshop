---
title: 'Execute the state machine'
weight: 103
---

- Click on **Start execution** and use the below as your input payload.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "Testing AWS SDK integration"
}
:::

- Inspect the **Execution event history** to view a list of S3 buckets. You should find one that starts with `univesalsdkintegrationbucket-`.

::alert[**Congratulations!** You have successfully completed an AWS SDK service integration.]{type="success"}
