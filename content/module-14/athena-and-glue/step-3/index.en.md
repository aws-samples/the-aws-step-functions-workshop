---
title: 'Crawler Workflows'
weight: 3
---

There are 3 state machines deployed for this module.

1. Create Dataset - this state machine will create the dataset in the S3 bucket that we’ll use for the data pipeline.
2. Run Crawler - this state machine will crawl the S3 dataset to identify the metadata and make it accessible with Glue Data Catalog
3. Data Reporting - this state machine will orchestrate multiple Athena queries on the dataset and send out the results to an SNS topic to be consumed by any subscriber.

### Creating the sample dataset in S3

In this module we'll create a sample data set with Step Functions AWS SDK integration with S3. Step Functions will use the `PutObject` call to insert sample data into S3.

![Create Data](/static/img/module-13/createdata_statemachine.png)

1. To create the dataset, you choose Start execution from the toolbar for the create-dataset state machine, then choose Start execution again in the dialog box. This runs the state machine and creates the dataset in S3.
2. Navigate to the S3 console to view the newly created dataset.
3. Open the data/daily-user-summaries folder within the S3 data bucket to examine the sample dataset
![View Data](/static/img/module-14/GlueAthena-S3Data.png)

### Crawling the data set

You now use AWS Glue crawlers to analyze these datasets and make them available to query.

![Glue Crawler](/static/img/module-13/crawler_statemachine.png)

1. To crawl the dataset, you choose Start execution from the toolbar for the crawl-dataset state machine, then choose Start execution again in the dialog box. This runs the state machine and crawls the dataset in S3.
2. The state machine periodically checks the current state of the crawl job to see it's complete. Before analyzing the data, you want to make sure all the data was crawled so that the results of the Athena query will be based on the most up to date data. 
3. Navigate to the Glue Data Catalog to see the metadata of your S3 dataset.

![Glue Data Catalog](/static/img/module-14/GlueAthena-GlueDataCatalog.png)

### Execute Athena Queries

You'll now use Athena to analyze the sample dataset and post the results to an SNS topic.

![Create Data](/static/img/module-13/query_statemachine.png)

1. Now, navigate to the Athena console where you can see the database and tables created by your crawlers. Note that AWS Glue recognized the partitioning scheme and included fields for year, month, and date in addition to user and usage fields for the data contained in the JSON files.
2. To execute the Athena queries, you choose Start execution from the toolbar for the execute-queries state machine, then choose Start execution again in the dialog box
3. You should see a message was posted to the SNS Topic with the results of the Athena queries.

Note that the Usage 2021 Athena query scanned far fewer bytes and executed faster compared to the All Time Usage Query. This is because Athena used the partitioning information to avoid querying the full dataset. While the differences in this example are small, for real-world datasets with terabytes of data, your cost and latency savings from partitioning data can be substantial.

The disadvantage of a partitioning scheme is that new folders are not included in query results until you add new partitions. Re-running your crawler identifies and adds the new partitions and using Step Functions to orchestrate these crawlers makes that task simpler.

### Operational Guidance

In a production environment, you can schedule these State Machines to run nightly after daily data loads. The Glue Crawler state machine will incrementally crawl the new data and make it available to query via Athena. You can schedule the Athena Queries state machine to run after the Glue Crawler state machine to include the latest data as part of its results. You can use EventBridge to schedule State Machines or route S3 event notifications via EventBridge to trigger the State Machine workflows.

Data engineers should consider following an event-driven approach in handling results of the Athena queries. Publishing the results of the Athena Query state machine to SNS or EventBridge offers both greater extensibility and simplicity for developers adding new functionality in the future such as dashboards or query result notifications. It can help alleviate the problems associated with monolithic applications. It’s also easier and safer to deploy changes to a single microservice consuming the query results without needing to re-deploy the entire application. Developers would only understand their own service rather than the complete architecture of the application.