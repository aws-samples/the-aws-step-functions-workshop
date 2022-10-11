---
title: 'Execute the state machine'
weight: 113
---

- Click on **Start execution** and use the below as your input payload.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "I am very happy to learn about Step Functions!"
}
:::

- Inspect the **Execution event history** to view a list events and find one called **TaskSucceeded**. Click to expand this event and you should find the sentiment detected for your comment.
- Feel free to execute the state machine again with other input payloads in the Comment field and view the results of Comprehend's sentiment analysis. 

::alert[**Congratulations!** You have successfully completed an AWS SDK service integration.]{type="success"}
