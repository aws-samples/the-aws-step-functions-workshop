---
title: 'Tester le projet'
weight: 125
---

Après avoir créé votre API REST API Gateway avec une machine à états Express synchrone comme intégration backend, vous pouvez tester l'API.

### Tester l'API déployée à l'aide de la console API Gateway

1. Ouvrez la [Console Amazon API Gateway](https://console.aws.amazon.com/apigateway/) et connectez-vous.
2. Choisissez votre API REST nommée `CDKStepFunctionsRestApi`.
3. Dans le volet **Ressources**, vous pouvez sélectionner la méthode que vous souhaitez tester. Cliquez sur la méthode `ANY`.
   ![API GATEWAY ANY](/static/img/module-10/api-gateway-testing.png)
4. Dans le volet **Exécution de la méthode**, dans la zone **Client**, choisissez **TEST**.
5. Choisissez **POST** dans le menu déroulant de la **Méthode**. Copiez/collez le JSON ci-dessous dans le champ **Request Body**.
   :::code{showCopyAction=true showLineNumbers=true language=json}
   {
   "key": "Hello Step Functions!"
   }
   :::
6. Cliquez sur **Tester**. Les informations suivantes seront affichées :

    - **Request** est le chemin de la ressource qui a été appelée pour la méthode.
    - **Statut** est le code de statut HTTP de la réponse.
    - **Latence** est le temps entre la réception de la demande de l'appelant et la réponse renvoyée.
    - **Response Body** est le corps de la réponse HTTP.
    - **En-têtes de réponse** sont les en-têtes de réponse HTTP.
    - Les **journaux** sont les entrées Amazon CloudWatch Logs simulées qui auraient été écrites si cette méthode avait été appelée en dehors de la console API Gateway.
    
  ::alert[Bien que les entrées CloudWatch Logs soient simulées, les résultats de l'appel de méthode sont réels.]{header="Note"}

**Corps de la réponse** devrait être :

```bash
"Hello back to you!"
```

### Tester l'API déployée à l'aide de cURL

- Ouvrez un nouveau terminal dans votre environnement AWS Cloud9.
- Copiez la commande cURL suivante et collez-la dans la fenêtre du terminal, en remplaçant `<api-id>` par l'ID d'API de votre API et `<region>` par la région où votre API est déployée. Vous avez peut-être copié cette URL à partir de la sortie CloudFormation à l'étape précédente. Vous pouvez également trouver l'URL d'appel complète dans la console API Gateway en accédant à **Stages > prod**.

```bash
curl -X POST\
 'https://<api-id>.execute-api.<region>.amazonaws.com/prod' \
 -d '{"key":"Hello Step Functions"}' \
 -H 'Content-Type: application/json'
```

La sortie **Corps de la réponse** doit être :

```bash
"Hello back to you!"
```

::alert[**Félicitations !** Vous avez terminé ce module avec succès.]{type="success"}
