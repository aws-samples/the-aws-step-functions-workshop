---
title: 'Exécuter une exécution synchrone via API Gateway'
weight: 96
---

## Rendre l'intégration synchrone

1. Accédez à la console API Gateway et sélectionnez l'API créée pour ce module.
   ![API Console](/static/img-fr/module-7/api-console.png)
2. Dans la liste des ressources, recherchez la ressource `execution` et cliquez sur `POST`
   ![API Execution](/static/img-fr/module-7/api-execution-new.png)
3. Cliquez sur `Demande d'intégration`
4. Modifiez `Action` en cliquant sur le crayon gris et changez-le en `StartSyncExecution` et cliquez sur le bouton de mise à jour
   ![API Execution Sync](/static/img-fr/module-7/api-integration-setup-sync.png)
5. Testez à nouveau votre API.
6. Vous remarquerez un `Corps de la réponse` plus grand avec plus de détails sur l'exécution de la machine à états, y compris `input` et `output`.
   ![API Test Result Sync](/static/img-fr/module-7/api-test-result-sync-4.png)

::alert[**Félicitations !** Vous venez d'exécuter une intégration synchrone entre API Gateway et Step Functions.]{type="success"}
