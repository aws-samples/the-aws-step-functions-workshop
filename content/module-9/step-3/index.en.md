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
A workflow that contains an AWS SDK service integration with Amazon S3.
```

6. One the left hand side **Actions** menu, use the search bar and search for `ListBuckets`. You should see the **S3 ListBuckets** action show up.

7. Drag & drop `ListBuckets` from the **Actions** section on the left side to the designer form where it says `Drag first state here`.
   ![](/static/img/module-9/list-bucket.png)
   ![](/static/img/module-9/list-bucket-state.png)

8. Click on the S3 action. Use the defaults for **Configuration, Input, Output and Error handling**. Click the **Definition** button to review the ASL syntax you will generate.

9. Now click on **Next** and review the generated code. Click on **Next** again.

10. Provide a name to your state machine, `ListBucketMachine`.

11. Click the **Choose existing role** button and select `UniversalSDKRoleNameforStepfunctions` from the drop down.

![](/static/img/module-9/iam.png)

12. Now click on **Create state machine**.

13. You have successfully created the state machine.
