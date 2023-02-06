---
title: 'Vérifier le workflow'
weight: 43
---

Accédez à [Step Functions dans la console](https://console.aws.amazon.com/states/home) et cliquez sur la machine à états dont le nom commence par **"RequestResponseStateMachine"**. Dans cet exemple, nous attendrons un délai spécifié, puis nous publierons une notification dans une rubrique SNS en utilisant le modèle 'Réponse à la requête'.

Lorsque vous spécifiez un service dans le champ `Resource` de votre tâche et que vous ne fournissez que la ressource, Step Functions attendra une réponse HTTP de l'API du service, puis passera immédiatement à l'état suivant. Step Functions n'attend pas la fin de l'exécution de la tâche. Il s'agit du modèle 'Réponse à la requête'.

Vérifier la définition dans Workflow Studio (cliquez sur **Modifier** puis **Workflow Studio**):

![Workflow du module 2](/static/img/module-2/workflow.png)

Cliquez sur **Définition**. Remarquez le champ `"Resource"` de la tâche ci-dessous. Ce code désigne un modèle d'intégration de service 'Réponse à la requête'.

![Code du module 2](/static/img/module-2/code.png)
