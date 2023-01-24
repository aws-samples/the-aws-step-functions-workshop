---
title: "Revue du workflow"
weight: 32
---

Accédez à [Step Functions depuis la console](https://console.aws.amazon.com/states/home) et cliquez sur la machine à états dont le nom commence par **TimerStateMachine**. Dans cet exemple d'application, nous exécuterons une tâche après avoir attendu un délai spécifié. Cliquez sur **Modifier**, puis cliquez sur le bouton de Workflow Studio :

![Boutton Workflow Studio](/static/img-fr/module-1/workflow-studio.png)

Passez en revue la définition dans Workflow Studio :

![Workflow du module 1](/static/img/module-1/workflow.png)

La machine à états est définie à l'aide d'Amazon States Language (ASL). Cliquez sur le bouton **Définition** pour afficher le code ASL. Vous pouvez voir que l'ASL contient un état `Wait`.

![Code du module 1](/static/img/module-1/code.png)
