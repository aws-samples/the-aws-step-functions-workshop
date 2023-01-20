---
title: 'Loading the dataset into your AWS account'
weight: 3
---

The first step is to use the CopyNOAAS3DataStateMachine to copy a subset of the source data into an S3 bucket in your account.

1. Navigate to the CopyNOAAS3DataStateMachine and click on **Start Execution**. 
2. You should see the state machine execution complete successfully within a few seconds.
3. Navigate to the dmap-demo-noaadatabucket bucket to confirm the files are in the bucket.

### Let's explore the dataset

The csv files we copied into the S3 bucket contain daily weather data between 1929 and 1937 for each city. The excerpt below shows the columns we're interested in.

CSV File for Lerwick, UK in October 1929:

| Station        | Date       | Name        | Temp |
| ---            | ---        | ---         | ---  |
| **3005099999** | 1929-10-02 | LERWICK, UK | 49.5 |
| **3005099999** | 1929-10-03 | LERWICK, UK | 49.0 |
| **3005099999** | 1929-10-04 | LERWICK, UK | 45.7 |

CSV File for Dyce, UK in October 1929:

| Station        | Date       | Name        | Temp |
| ---            | ---        | ---         | ---  |
| **3091099999** | 1929-10-02 | DYCE, UK    | 50.5 |
| **3091099999** | 1929-10-03 | DYCE, UK    | 48.0 |
| **3091099999** | 1929-10-04 | DYCE, UK    | 43.8 |

If we wanted to know the city with the highest average temperature during October 1929, we would go through each line of each city's CSV files and compare the averages for that month. Calculating averages of large datasets with gigabytes of temperature data across many locations is would take hours in a single threaded process. The new distributed map state can launch up to ten thousand parallel workflows to iterate over millions of objects such as the csv files in this module, logs or images stored in Amazon S3.

In the next step, you will build a workflow with a Distributed Map state to analyze the dataset.