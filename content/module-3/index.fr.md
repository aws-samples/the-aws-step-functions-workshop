---
title: 'Module 3 - Run a Job (.sync)'
weight: 50
---

Pour les services intégrés tels qu'AWS Batch et Amazon ECS, Step Functions peut attendre la fin d'une tâche avant de passer à l'état suivant. Ce modèle d'orchestration de tâches est appelé [Run a Job (.sync)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-sync) dans la documentation. Pour voir une liste des services intégrés qui prennent en charge la synchronisation, consultez [Optimized integrations for Step Functions](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/connect-supported-services.html).

Pour voir un exemple de projet de calcul haute performance (HPC) utilisant AWS Batch, Step Functions et Run a Job (.sync), consultez [ce blog](https://aws.amazon.com/blogs/compute/orchestrating-high-performance-computing-with-aws-step-functions-and-aws-batch/).

Dans ce module, vous configurerez et exécuterez une tâche synchronisée à l'aide de **Run a Job (.sync)**.

**Durée estimée : 10 minutes**
