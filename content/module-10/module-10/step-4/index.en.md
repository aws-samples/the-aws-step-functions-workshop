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

- Inspect the **Execution event history** and verify if you see an s3 bucket in the output which starts with `univesalsdkintegrationbucket-`.

::alert[**Congratulations!** You have successfully completed the module.]{type="success"}
