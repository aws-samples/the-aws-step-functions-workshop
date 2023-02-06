---
title: 'Exécuter le workflow initial'
weight: 63
---

Accédez à [Step Functions dans la console](https://console.aws.amazon.com/states/home) et cliquez sur la machine à états dont le nom commence par **"WaitForCallbackStateMachine"**. L'architecture de l'application utilisée pour ce module est présentée dans le schéma ci-dessous. Cette machine à états envoie un message à SQS en utilisant le modèle **Attente d'un rappel** et transmet un jeton de tâche. SQS envoie ensuite le message et le jeton à une fonction Lambda. Cependant, le rappel (étape 3 dans le diagramme ci-dessous) n'est pas encore implémenté dans la fonction Lambda.

![Architecture du module 4](/static/img-fr/module-4/callback-architecture.png)

Exécutez la machine à états en utilisant l'entrée par défaut. Notez que l'exécution sera interrompue indéfiniment à l'état `Start Task and Wait For Callback`.

![Workflow du module 4](/static/img/module-4/initial-workflow.png)
