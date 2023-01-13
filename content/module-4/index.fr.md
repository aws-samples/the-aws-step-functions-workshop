---
title: "Module 4 - Attendre un rappel avec le jeton de tâche"
weight: 60
---

La fonctionnalité [Attendre un rappel](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/connect-to-resource.html#connect-wait-token) permet de suspendre un workflow indéfiniment jusqu'à ce qu'un jeton de tâche soit renvoyé.

Par exemple, une tâche peut nécessiter une approbation humaine, s'intégrer à un service tiers ou appeler un système hérité. Pour de telles applications, une tâche peut transmettre un jeton unique au service intégré et s'arrêter. La tâche ne reprendra que lorsqu'elle recevra le jeton de tâche via un appel à l'API `SendTaskSuccess` ou `SendTaskFailure`. Pour voir une liste des services intégrés qui prennent en charge l'attente de rappel (`.waitForTaskToken`), consultez [Intégrations optimisées pour Step Functions](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/connect-supported-services.html).

Dans ce module, vous implémenterez un modèle d'orchestration **Attente d'un rappel**

**Durée estimée : 15 minutes**