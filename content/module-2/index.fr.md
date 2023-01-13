---
title: 'Module 2 - Réponse à la requête'
weight: 40
---

Lorsque Step Functions appelle un autre service à l'aide de l'état `Task`, le modèle par défaut est [Réponse à la requête](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/connect-to-resource.html#connect-default). Avec ce modèle d'orchestration de tâches, Step Functions appellera le service, puis passera immédiatement à l'état suivant. L'état `Task` n'attendra pas la fin de l'exécution de la tâche sous-jacente.

Dans ce module, vous exécuterez une `Task` en utilisant le modèle 'Réponse à la requête'.

**Durée estimée : 15 minutes**