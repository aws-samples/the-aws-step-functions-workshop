---
title: "Vue d'ensemble de l'architecture"
weight: 73
---

Ce module illustre le parallélisme dynamique à l'aide des états Map et Choice. Ce module contient les ressources suivantes :

- Deux fonctions AWS Lambda

- Une file d'attente Amazon Simple Queue Service (Amazon SQS)

- Une rubrique Amazon Simple Notification Service (Amazon SNS)

- Une table Amazon DynamoDB

- Une machine à états AWS Step Functions

Dans ce module, Step Functions appelle une fonction AWS Lambda qui récupère les messages d'une file d'attente Amazon SQS. La fonction Lambda renvoie ensuite un tableau JSON de ces messages à un état Map. L'état Map parcourt chaque message du tableau en créant dynamiquement des branches de workflows distinctes. Chaque branche de workflow écrit un message dans DynamoDB, puis appelle une deuxième fonction Lambda pour supprimer le message d'Amazon SQS. Enfin, la branche publie le message dans la rubrique Amazon SNS.

![Workflow visuel](/static/img/module-5/visual-workflow.png)

En savoir plus sur les [intégrations de services Step Functions](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-service-integrations.html).
