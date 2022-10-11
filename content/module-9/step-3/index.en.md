---
title: 'Create the state machine and provision resources'
weight: 112
---

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in your AWS console. Make sure you are in the correct region.

2. If you are not on the `State machines` page, click on `State machines` on the left side menu and click **Create state machine**

3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Standard** and click on `Next`.
   ![Studio](/static/img/module-6/studio-selection.png)

4. You should see the designer studio now which will look like this.
   ![](/static/img/module-6/studio-designer.png)

5. Enter a `Comment` on the right side: 

```bash
A workflow that contains an AWS SDK service integration with Amazon Comprehend.
```

6. On the left hand side **Actions** menu, use the search bar and search for `DetectSentiment`. You should see the **Comprehend DetectSentiment** action show up.

7. Drag & drop `DetectSentiment` from the **Actions** section on the left side to the designer form where it says `Drag first state here`.
   ![](/static/img/module-9/detect-sentiment.png)
   ![](/static/img/module-9/detect-sentiment-state.png)

8. Click on the Comprehend action.
9. Update the API Parameters in the **Configuration** section to use the following:
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "LanguageCode": "en",
  "Text.$": "$.Comment"
}
:::

The state machine will pass the execution input's Comment value to Comprehend for sentiment analysis.

10. Use the defaults for **Input, Output and Error handling**. Click the **Definition** button to review the ASL syntax you will generate.
    
11. Now click on **Next** and review the generated code. Click on **Next** again.
12. Provide a name to your state machine, `DetectSentimentMachine`.

13. Click the **Choose existing role** button and select `UniversalSDKRoleNameforStepfunctions` from the drop down.

![](/static/img/module-9/iam.png)

14. Now click on **Create state machine**.

15. You have successfully created the state machine.
