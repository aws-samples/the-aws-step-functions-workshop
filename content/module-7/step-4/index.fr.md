---
title: "Construire une machine à états avec un état Parallel et l'intégrer à API Gateway"
weight: 94
---

### Créer la machine à états

Suivez les étapes ci-dessous pour créer une machine à états à l'aide de Workflow Studio.

1. Accédez à [Step Functions](https://console.aws.amazon.com/states/home) dans votre console AWS. Assurez-vous d'être dans la bonne région.
2. Cliquez sur **Créer une machine d'état**.
3. Pour `Choisir la méthode de création`, sélectionnez `Concevoir visuellement votre flux de travail`, sélectionnez `Express` come type de machine à états et cliquez sur **Suivant**.
   ![Sélection studio](/static/img-fr/module-7/studio-selection.png)
4. Vous devriez voir Workflow Studio.
   ![Studio Designer](/static/img-fr/module-7/studio-designer.png)
5. Entrez un `Commentaire` sur le côté droit :

```bash
A step functions workflow that executes tasks in parallel.
```

6. Faites glisser et déposez un état `Parallel` de la section **Flux** sur le côté gauche du designeur vers là où il est écrit `Faites glisser le premier état ici`.
   ![Ajouter un état parallèle](/static/img-fr/module-7/add-parallel-state.png)
7. Les trois fonctions Lambda de ce module doivent être déployées sur votre compte. Ajoutez une action pour appeler la première fonction Lambda.

- Faites glisser et déposez `AWS Lambda Invoke` de la section **Actions** sur le côté gauche du designeur vers là où il est écrit `Déposez l'état ici`.
  ![Appeler la fonction Lambda 1](/static/img-fr/module-7/lambda-invoke-function1.png)
- Dans l'onglet **Configuration** du designeur, entrez `SumValues` pour le nom de l'état.
- Dans la section `Paramètres de l'API`, sélectionnez dans le menu déroulant de `Nom de la fonction` la fonction avec `SumFunction` dans le nom.
  ![Configuration Sum State](/static/img-fr/module-7/configuration-sum-state.png)
- Dans l'onglet `Sortie`, décochez l'option `Filtrer la sortie avec le chemin de sortie` et cochez l'option `Transformer le résultat avec ResultSelector`, puis collez le JSON suivant dans la zone de texte :

  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "sum.$": "$.Payload.sum" }
  :::
  ![Output Sum State](/static/img-fr/module-7/output-sum-state.png)

8. Ajoutez une action pour appeler la deuxième fonction Lambda.

- Faites glisser et déposez `AWS Lambda Invoke` de la section **Actions** sur le côté gauche du designeur vers là où il est écrit `Déposez l'état ici`.
  ![Appeler la fonction Lambda 2](/static/img-fr/module-7/lambda-invoke-function2.png)
- Dans l'onglet **Configuration** du designeur, saisissez `AverageValues` pour le nom de l'état.
- Dans la section `Paramètres de l'API`, sélectionnez dans le menu déroulant de **Nom de la fonction** la fonction avec `AvgFunction` dans le nom.
  ![Configuration Avg State](/static/img-fr/module-7/configuration-avg-state.png)
- Dans l'onglet `Sortie`, décochez l'option `Filtrer la sortie avec le chemin de sortie` et cochez l'option `Transformer le résultat avec ResultSelector`, puis collez le JSON suivant dans la zone de texte :
  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "avg.$": "$.Payload.avg" }
  :::
  ![Output Avg State](/static/img-fr/module-7/output-avg-state.png)

9. Ajoutez une action pour appeler la troisième fonction Lambda.

- Faites glisser et déposez `AWS Lambda Invoke` de la section **Actions** sur le côté gauche vers le formulaire du concepteur entre les deux actions existantes.
  ![Appeler la fonction Lambda 3](/static/img-fr/module-7/lambda-invoke-function3.png)
- Dans l'onglet **Configuration** du designeur, entrez `MaxMinValues` pour le nom de l'état.
- Dans la section `Paramètres de l'API`, sélectionnez dans le menu déroulant de **Nom de la fonction** celui dont le nom contient `MaxMinFunction`.
  ![Max Min State](/static/img-fr/module-7/configuration-maxmin-state.png)
- Dans l'onglet `Sortie`, décochez l'option `Filtrer la sortie avec le chemin de sortie` et cochez l'option `Transformer le résultat avec ResultSelector`, puis collez le JSON suivant dans la zone de texte :
:::code{showCopyAction=true language=json}
{
"max.$": "$.Payload.max",
"min.$": "$.Payload.min"
}
:::
  ![Output Max Min State](/static/img-fr/module-7/output-maxmin-state.png)

10. Cliquez sur **Suivant** et passez en revue le code généré, puis cliquez à nouveau sur **Suivant**.

- Donnez un nom à cette machine à états : `ParallelProcessingMachine`. Choisissez un rôle IAM existant avec le nom contenant `StepFunctionsIamRole`.
- Laissez les autres valeurs par défaut et cliquez sur **Créer une machine d'état**.
  Vous avez maintenant une machine à états qui peut exécuter des calculs parallèles. Copiez l'ARN de la machine à états et enregistrez-le. Vous en aurez besoin pour créer l'intégration avec API Gateway.

### Configuration de l'intégration entre API Gateway et Step Functions

1. Accédez à la [console API Gateway](https://console.aws.amazon.com/apigateway/home) et sélectionnez l'API créée pour ce module : `API Gateway State Machine integration`.
   ![API Console](/static/img-fr/module-7/api-console.png)
2. Dans la liste des ressources, recherchez la ressource `/execution` et cliquez sur `POST`
   ![API Execution](/static/img-fr/module-7/api-execution.png)
3. Cliquez sur `Demande d'intégration`
4. Pour le `Type d'intégration`, sélectionnez `Service AWS`
5. Configurez l'intégration :

- **AWS Region**: sélectionnez la région AWS dans laquelle vous avez créé la machine à états
- **AWS Service**: sélectionnez `Step Functions` dans la liste déroulante
- **HTTP Method**: sélectionnez `POST`
- **Type d'Action**: sélectionnez `Utiliser le nom de l'action`
- **Action**: tapez `StartExecution`
- **Execution role**: trouver dans [IAM](https://console.aws.amazon.com/iamv2/home) le rôle avec `IntegrationIamRole` dans son nom et utiliser l'ARN de ce rôle
  ![Configuration de l'intégration de l'API](/static/img-fr/module-7/api-integration-setup.png)
- Cliquez sur `Enregistrer`. Lorsque vous êtes invité à basculer vers une intégration AWS, cliquez sur `Ok`.
  Vous avez maintenant configuré une intégration entre API Gateway et Step Functions.
