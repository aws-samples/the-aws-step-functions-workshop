---
title: 'Replace Steps with a Nested Express Workflow'
weight: 154

---

Let's replace the steps in our Standard workflow with a nested Express workflow. An Express workflow containing these steps has already been created in your account, with a name beginning with _ChildStateMachine_.

1. In the [Step Functions Console](https://console.aws.amazon.com/states/home), select “State machines” on the left-hand side and then click on the state machine with the name beginning with *ChildStateMachine*. From the “Details” box at the top, copy the ARN value, as you will use it in a subsequent step.  

2. Next, open the state machine with the name beginning with *ParentStateMachine*. Click Edit and then click the Workflow Studio button on the right-hand side to edit the state machine in Workflow Studio.  

3. Start by deleting the **Update Order History**, **Update Data Warehouse**, **Update Customer Profile**, and **Update Inventory** steps by selecting the steps and clicking **Delete all selected states**.  

    ![Delete existing workflow steps](/static/img/module-13/delete-steps-from-workflow.png)

4. Now, add an AWS Step Functions StartExecution step, in between **Notify Payment Success** and **Ship the Package** by dragging from the palette on the left. If StartExecution it is not available in the “Most Popular” section, type StartExecution in the search bar at the top of the palette.  

    ![Add StartExecution step](/static/img/module-13/add-start-execution-step.png)

5. Click on the **Step Functions StartExecution** step you just added to configure it to invoke the Express workflow. To make it clear what this nested workflow does, update the “State name” to read “Workflow to Update Backend Systems.”  

6. Next, in the “API Parameters” box, replace the value for the “StateMachineArn” attribute with the ARN you copied in step 1. This tells Step Functions which nested workflow to execute. You can also optionally remove the “StatePayload” attribute, as it is not used by the nested workflow.  

    ![Configure nested Express workflow](/static/img/module-13/configure-nested-express-workflow.png)

7. When you’ve made the updates, click the **Apply and Exit** button and then the **Save** button.  

8. You may receive a warning that the changes could affect which resources your state machine needs to access and therefore, updates to the IAM role used by your state machine may be required. For simplicity, the role already contains the required permissions, but in the real world, you should make sure to review the IAM role used by your state machine.  

9. Run the updated state machine by clicking the **Start Execution** button in the upper right corner. The state machine does not require any input - you can leave the “Comment” attribute that’s included by default, if you wish. Click **Start Execution**. You can now watch the state machine as the steps are executed and you should see a fully green diagram. Now, click the “State Machines” link on the left side and choose the workflow starting with _ChildStateMachine_. On the “Monitoring” tab, you should see a value of 1 for the “Executions Started” metric, and a value of 1 for the “Executions Succeeded” metric, indicating the nested workflow was executed successfully.  

    ![Child Express workflow execution stats](/static/img/module-13/child-state-machine-execution-stats.png)

::alert[**Congratulations!** You replaced several Standard workflow steps with a nested Express workflow!]{type="success"}
