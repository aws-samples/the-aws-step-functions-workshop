---
title: 'Data Processing with AWS Glue and Amazon Athena'
weight: 1
---

Organizations generate terabytes of data every day in a variety of semistructured formats. AWS Glue and Amazon Athena can give you a simpler and more cost-effective way to analyze this data with no infrastructure to manage. AWS Glue crawlers identify the schema of your data and manage the metadata required to analyze the data in place, without the need to transform this data and load into a data warehouse. Amazon Athena is an interactive query service that makes it easier to analyze your data using standard SQL.

The timing of when your crawlers run and complete is important. You must ensure the crawler runs after your data has updated and before you query it with Athena or analyze with an AWS Glue job. If not, your analysis may experience errors or return incomplete results.

You can use Step Functions to orchestrate your crawler workflows and Athena queries to ensure correct reporting results and have an instant visual understanding of the application and any errors that might occur during execution.

**Estimated Duration: 15 minutes**