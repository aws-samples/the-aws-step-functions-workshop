---
title: 'Large-Scale Parallelization with Distributed Map'
weight: 2
---

In this module, the Step Functions workflow uses a Map state in Distributed mode to process a list of S3 objects in an S3 bucket. Step Functions iterates over the list of objects and then launches thousands of parallel workflows, running concurrently, to process the items.

The dataset used in this module is a small subset of the 37+ GB of NOAA Global Surface Summary of Day. The application code in this example finds the weather station that has the highest average temperature on the planet each month. This data set is interesting for a few reasons:

The data is organized by station/day. Each weather station will have a single record with averages per day. This example Step Function workflow will find the highest average temperature across all stations by month. That is, it answers the question: "What place on earth recorded the hightest average daily temperature within a given month?"
There are over 558,000 CSV files in the data set at over 37 GB. The average CSV file size is 66.5 KB.
The CSV files are relatively simple to understand and parse.

Review the documentation:
- [AWS Blog: Step Functions Distributed Map – A Serverless Solution for Large-Scale Parallel Data Processing](https://aws.amazon.com/blogs/aws/step-functions-distributed-map-a-serverless-solution-for-large-scale-parallel-data-processing/)
- [Documentation: Using Map state in Distributed mode](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-asl-use-map-state-distributed.html)
- [Video: AWS Step Functions large-scale parallel data processing | Serverless Office Hours](https://www.youtube.com/watch?v=iZ2aMAoUL24)

**Estimated Duration: 30 minutes**