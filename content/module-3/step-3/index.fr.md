---
title: 'Exécuter une tâche asynchrone'
weight: 53
---
Accédez à [Step Functions depuis la console](https://console.aws.amazon.com/states/home) et cliquez sur la machine à états dont le nom commence par **"BatchJobNotification"**. Ce workflow soumet une tâche AWS Batch. Dans son état initial, le travail est asynchrone. La machine à états soumet la tâche AWS Batch mais n'attend pas la fin de la tâche. Au lieu de cela, elle passe immédiatement à l'état suivant et envoie un message `Notify Success` à une rubrique Amazon SNS.

Voici à quoi ressemble le workflow initial :

![workflow initial du module 3](/static/img/module-3/initial-workflow.png)

Voici à quoi ressemble la définition de tâche pour la tâche AWS Batch. Prenez note du paramètre `"Resource"`.

![Code module 3](/static/img/module-3/initial-code.png)

Cliquez maintenant sur **Démarrer l'exécution** et utilisez l'entrée par défaut. Le service AWS Batch effectue une tâche, qui peut prendre une minute ou plus pour se terminer. Remarquez à quelle vitesse cette exécution se termine.

![Graph initial](/static/img/module-3/initial-graph.png)

Imaginons maintenant que nous ayons besoin que notre machine à états reste synchronisée avec AWS Batch et ne continue qu'une fois la tâche terminée.
