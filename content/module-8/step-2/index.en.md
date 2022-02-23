---
title: 'Create the state machine and provision resources'
weight: 102
---

1. Navigate to Step Functions in your AWS console. Make sure you are in the same AWS region that is assigned for this session.

2. If you are not on the `State machines` page, click on `State machines` on the left side menu and click **Create state machine**

3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Standard** and click on `Next`.
   ![Studio](/static/extra-credit-2-studio-selection.png)

4. You should see the designer studio now which will look like this.
   ![](/static/extra-credit-2-studio-designer.png)

5. For `Comment` on the right side, enter `A step functions example showing MAP and Choice state implementation`.

6. One the left hand side **Actions** menu, use the search bar and search for `ListBuckets`. You should see the **S3 ListBuckets** action show up.

7. Drag & drop `ListBuckets` from the **Actions** section on the left side to the designer form where it says `Drag first state here`.
   ![](/static/extra-credit-3-list-bucket.png)
   ![](/static/extra-credit-3-list-bucket-state.png)

8. Keep **Configuration, Input, Output and Error handling** as it is, however for any API call you can pass the required API parameters. Also, take a look at the **Integration type and Definition**.

9. Now click on **Next** and review the generated code. Click on **Next** again.

10. Provide a name to your state machine, `UniversalSDKIntegration-sm`.

11. Under permissions choose **Choose existing role** and select `UniversalSDKRoleNameforStepfunctions` from the drop down.

![](/static/extra-credit-3-IAM.png)

12. Now click on **Create state machine**.

13. You have successfully created the state machine.
