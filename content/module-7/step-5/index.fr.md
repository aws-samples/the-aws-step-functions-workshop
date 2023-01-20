---
title: 'Exécuter une exécution asynchrone via API Gateway'
weight: 95
---

1. Accédez à la console API Gateway et sélectionnez l'API créée pour ce module.
   ![API Console](/static/img-fr/module-7/api-console.png)
2. Dans la liste des ressources, recherchez la ressource `execution` et cliquez sur `POST`
   ![API Execution New](/static/img-fr/module-7/api-execution-new.png)
3. Cliquez sur `Tester`
4. Au bas de la page, vous trouverez un champ appelé `Corps de la demande`, collez-y le JSON suivant et remplacez l'exemple `stateMachineArn` par l'ARN de votre State Machine.
:::code{showCopyAction=true language=json}
{
"input": "{\"data\": [20,40,60,10,9]}",
"name": "MyExecution",
"stateMachineArn": "arn:aws:states:us-east-1:123456789012:stateMachine:ParallelProcessingMachine"
}
:::

   ![API Test](/static/img-fr/module-7/api-test.png)
5. Cliquez sur `Tester`.
6. Regardez le `Corps de la réponse`. Notez qu'il inclut des références à `executionArn` et à `startDate`. Ces réponses sont renvoyées car la machine à états a été exécutée de manière asynchrone.

   ![Résultat du test API](/static/img-fr/module-7/api-test-result.png)

::alert[**Félicitations !** Vous venez d'exécuter une intégration asynchrone entre API Gateway et Step Functions.]{type="success"}
