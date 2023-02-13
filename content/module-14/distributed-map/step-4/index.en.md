---
title: 'Creating the data analysis workflow'
weight: 4
---

In this step, you'll create a workflow in Workflow Studio to analyze the weather data using the Distributed Map state.

We've provided the data processing code to you in the CloudFormation stack deployed for this module. The workflow you'll build orchestrates the parallel processing of the weather data. The Distributed Map state runs a child workflow execution for a subset of the data (Configurable using Item Batching); each child workflow execution will execute the data processing code for calculating the highest temperature averages in a month within that subset. After the every child workflow execution completes, we'll use the Reducer Lambda function to get the highest temperature averages across the entire dataset.

![Distributed Map Architecture](/static/img/module-14/DistributedMap.png)

We've provided data processing code in the following Lambda functions:

* **TemperaturesFunction**: This Lambda function is executed by each child workflow execution of the Distributed Map state and calculates the highest average temperatures by location and city for a subset of the data.
* **ReducerFunction**: This Lambda function will compare the results of each execution of the TemperaturesFunction. For example, child workflow execution 1 may find that Los Angeles, California, USA had the highest temperature on "1931-07" (July, 1931) while child workflow execution 2 finds that Cairo, Egypt had the highest temperature on "1931-07". The reducer function will take a final pass through the outputs from all of the child workflows to find the correct highest temperature for the **entire** dataset.

### Creating the Workflow

1. Navigate to [Step Functions](https://console.aws.amazon.com/states/home) in your AWS console. Make sure you are in the correct region.

2. If you are not on the `State machines` page, click on `State machines` on the left side menu and click **Create state machine**

3. For `Choose authoring method` select **Design your workflow visually**, select state machine `Type` as **Standard** and click on `Next`.
4. Click on the patterns tab and drag **Process S3 objects** onto the Workflow Studio canvas.
![Distributed Map Pattern](/static/img/module-14/DistributedMap-Pattern.png)
5. Configure the Distributed Map state with the following values:
    | Setting        | Value      | Notes   |
    | ---            | ---        | ---     |
    | **Processing mode** | Distributed | Map State in distributed mode runs child workflow executions for each map iteration to achieve up to 10K concurrent workflows |
    | **Item source** | Amazon S3 | |
    | **S3 item source** | S3 object list | Since we have multiple CSV files we want to analyze, we'll use this item source as it uses S3 ListObjects to get a list a paginated list of objects in the bucket. |
    | **S3 bucket** | Use the *distributedmapworkshopdataset* bucket. | You can find the S3 bucket name in the CloudFormation stack resources tab for this module or use the *Browse S3 or enter S3 URI option* and look for *distributedmapworkshopdataset* with the Browse S3 button. |
    | **Enable batching** | Check this box | |
    | **Max items per batch** | 500 | Define the number of items to be processed by each child workflow execution |
    | **Set concurrency limit** | 500 | The Lambda burst concurrency maximum is 3000. You can modify this concurrency setting based on the capacity of your downstream systems. |
    | **Child execution type** | Express | Given each of these child workflow executions only take a few seconds to run, we can use Express workflows. |
    | **Set a tolerated failure threshold** | Expand **Additional configuration** to see this setting. Check this box | |
    | **Tolerated failure threshold** | 5% | Use this setting to consider a job *failed* if a minimum threshold of child workflow executions failed. This is useful if you have inconsistencies in your dataset. |
    | **Use state name as label in Map Run ARN** | Check this box | |
    | **Export Map state results to Amazon S3** | Check this box | |
    | **S3 Bucket** | Use the *distributedmapresultsbucket* bucket. | Use *Browse S3 or enter S3 URI option*. You can find the S3 bucket name in the CloudFormation stack resources tab for this module or look for the *distributedmapresults* bucket with the Browse S3 button. |
    | **Prefix** | results | Append the "results" prefix at the end of the S3 URI i.e. s3://*distributedmapresults* bucket/results |
6. Select the Lambda Invoke state within the Distributed Map state.
   1. Function name: *TemperaturesFunction*
   2. Payload: *Use state input as payload*
7. Drag another AWS Lambda Invoke task state onto the canvas **below** the Distributed Map state.
![Distributed Map Pattern](/static/img/module-14/DistributedMap-Reducer.png)
1. Configure the Lambda Invoke state with the following values:
   1. Function name: *ReducerFunction*
   2. Payload: *Use state input as payload*
2. Click on **Next** and review the generated ASL and click **Next** again.
3. Enter the a State machine name: `DistributedMap-WeatherAnalysis`. 
   1. If you don't use this exact name, you will receive an IAM error in the next step.
4.  For the Execution role, choose an existing role: `TemperatureStateMachineRole`
5.  Leave the rest of the defaults and click **Create state machine**.

::alert[In the next step, you'll execute the workflow and view the results of the data processing job.]{type="success"}

