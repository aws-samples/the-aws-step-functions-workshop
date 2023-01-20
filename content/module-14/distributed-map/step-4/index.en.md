---
title: 'Creating the data analysis workflow'
weight: 4
---

In this step, you'll create a workflow in Workflow Studio to analyze the weather data using the Distributed Map state.

We've provided the data processing code to you in the CloudFormation stack deployed for this module. The workflow you'll build orchestrates the parallel processing of the weather data. The Distributed Map state runs a sub-workflow for a subset of the data; each sub-workflow will execute the data processing code for calculate the highest temperature averages in a month within that subset. After the every sub-workflow completes, we'll use the Reducer Lambda function to get the highest temperature averages across the entire dataset.

![Distributed Map Architecture](/static/img/module-14/DistributedMap.png)

We've provided data processing code in the following Lambda functions:

* **TemperaturesFunction**: This Lambda function is executed by each sub-workflow of the Distributed Map state and calculates the highest average temperatures by location and city for a subset of the data.
* **ReducerFunction**: This Lambda function will compare the results of each execution of the TemperaturesFunction. For example, sub-workflow 1 may find that Los Angeles, California, USA had the highest temperature on "1931-07" (July, 1931) while sub-workflow 2 finds that Cairo, Egypt had the highest temperature on "1931-07". The reducer function will take a final pass through the outputs from all of the child workflows to find the correct highest temperature for the **entire** dataset.

### Creating the Workflow

1. Create a new workflow and navigate to Workflow Studio.
2. Click on the patterns tab and drag **Process S3 objects** onto the Workflow Studio canvas.
![Distributed Map Pattern](/static/img/module-14/DistributedMap-Pattern.png)
3. Configure the Distributed Map state with the following values:
    | Setting        | Value      | Notes   |
    | ---            | ---        | ---     |
    | **Processing mode** | Distributed | |
    | **Item source** | Amazon S3 | |
    | **S3 item source** | S3 object list | Since we have multiple CSV files we want to analyze, we'll use this item source as it uses S3 ListObjects to get a list a paginated list of objects in the bucket. |
    | **S3 bucket** | Use the *dmap-demo-noaadatabucket* bucket. | You can find the S3 bucket name in the CloudFormation stack resources tab for this module |
    | **Enable batching** | Check this box | |
    | **Max items per batch** | 500 | |
    | **Set concurrency limit** | 3000 | The Lambda burst concurrency maximum is 3000. You can modify this concurrency setting based on the capacity of your downstream systems. |
    | **Child execution type** | Express | Given each of these sub-workflows only take a few seconds to run, we can use Express workflows. |
    | **Set a tolerated failure threshold** | Check this box | |
    | **Tolerated failure threshold** | 5% | Use this setting to consider a job *failed* if a minimum threshold of sub-workflows failed. This is useful if you have inconsistencies in your dataset. |
    | **Use state name as label in Map Run ARN** | Check this box | |
    | **Export Map state results to Amazon S3** | Check this box | |
    | **S3 Bucket** | Use the *dmap-demo-resultsbucket* bucket. | You can find the S3 bucket name in the CloudFormation stack resources tab for this module |
4. Drag an AWS Lambda Invoke task state onto the canvas below the Distributed Map state.
![Distributed Map Pattern](/static/img/module-14/DistributedMap-Reducer.png)
5. Configure the Lambda Invoke state with the following values:
   1. Function name: *Reducer function*
   2. Payload: *Use state input as payload*

In the next step, you'll execute the workflow and view the results of the data processing job.