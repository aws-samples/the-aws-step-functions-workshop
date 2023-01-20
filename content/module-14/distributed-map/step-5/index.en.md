---
title: 'Run the workflow and view results'
weight: 5
---

1. Now go ahead and "Start execution" on this state machine using the default execution input.
2. The execution will take up to 1 minute to complete successfully.
3. In the execution details page, click on the Distributed Map state in the Graph View, then click on the Details tab.
![Distributed Map Pattern](/static/img/module-14/DistributedMap-JobRun.png)
4. Click on the Map Run link to view details of the Distributed Map execution.
5. This page provides a summary of the Distributed Map job.
![Distributed Map Pattern](/static/img/module-14/DistributedMap-JobRunDetails.png)
   * We can see that 1,000 files were processed successfully with 0 failures.
   * We can view the duration of each sub-workflow. You can see overlapping timestamps for the start and end times, indicating that the data was processed in parallel.
   * If you click on the execution name, you can use the Execution Input and output tab to view the input files for a sub-workflow and the execution output with details of the station with the highest average temperature for that month.
   * ![Distributed Map Pattern](/static/img/module-14/DistributedMap-SubWorkflowDetails.png)
6. The Distributed Map state will store the results of the Map Run into the results S3 bucket.
7. The Reducer function retrieves the data stored in the results S3 bucket and compares the highest average temperatures found in the S3 sub-workflows.
8. The Reducer function will store the results of the data analysis in the DynamoDB table **ResultsDynamoDBTable**. You can use the gear icon on the right side of the screen to select which columns you want to view.

![DynamoDB Results](/static/img/module-14/DistributedMap-DynamoDB-Results.png)

::alert[**Congratulations!** You used Distributed Map state to quickly process a large dataset using parallel processing.]{type="success"}