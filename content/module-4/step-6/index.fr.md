---
title: 'Exécuter le workflow avec rappel'
weight: 66
---

Revenez à [Step Functions](https://console.aws.amazon.com/states/home) et démarrez une nouvelle exécution de **WaitForCallbackStateMachine** en utilisant l'entrée par défaut. Cette fois, vous remarquerez que la machine à états termine son exécution car la fonction Lambda a effectué le rappel.

![Workflow du module 4](/static/img/module-4/modified-workflow.png)

::alert[**Félicitations!** Vous avez exécuté une machine à états avec le modèle **Attente d'un rappel**.]{type="success"}
