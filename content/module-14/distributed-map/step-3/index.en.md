---
title: "Let's explore the dataset"
weight: 3
---

Navigate to the S3 Bucket starting with the name **distributedmap-copydestination** to view a subset of the original NOAA source data.

The CSV files we copied into the S3 bucket contain daily weather data between 1929 and 1937 for each city. The excerpt below shows the columns we're interested in.

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

If we wanted to know the city with the highest average temperature during October 1929, we would go through each line of each city's CSV files and compare the averages for that month. Calculating averages of large datasets with gigabytes of temperature data across many locations would take hours in a single threaded process. The new distributed map state can launch up to ten thousand parallel workflows to iterate over millions of objects such as the CSV files in this module, logs or images stored in Amazon S3.

In the next step, you will build a workflow with a Distributed Map state to analyze the dataset.