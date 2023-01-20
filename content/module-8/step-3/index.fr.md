---
title: 'Gérer une erreur avec plusieurs tentatives'
weight: 103
---

Les états `Task` et `Parallel` peuvent avoir un champ nommé `Retry`, dont la valeur doit être un tableau d'objets appelés _réessayeurs_. Un réessayeur définit un certain nombre de tentatives, généralement à des intervalles de temps croissants.

Dans l'exercice ci-dessous, vous allez créer une définition ASL qui appelle une fonction Lambda. La fonction Lambda est conçue pour échouer. Vous implémenterez un `Retry` pour cette fonction, en définissant un nombre maximal de tentatives avec un temps d'attente exponentiel entre les tentatives.

1. Localisez la [fonction Lambda](https://console.aws.amazon.com/lambda/home) `ErrorHandlingCustomErrorFunction`. Copiez l'ARN de la fonction et passez en revue le code. Notez que le code est configuré pour générer une erreur.

   ![La fonction Lambda génère une FooError](/static/img/module-8/error-handling-lambda-foo-error.png)

2. Localisez maintenant la [machine à états](https://console.aws.amazon.com/states/home) `ErrorHandlingStateMachineWithRetry-...`. Cliquez sur son lien et cliquez sur le bouton **Modifier** dans le coin supérieur droit de l'écran.

3. Dans le champ `Resource`, remplacez la valeur actuelle par l'ARN de la fonction Lambda copiée à l'étape 1. Lorsque la machine à états appelle cette fonction, la fonction va échouer. Pour observer l'échec, cliquez sur `Enregistrer` puis sur **Démarrer une exécution**. Acceptez l'entrée par défaut et cliquez à nouveau sur **Démarrer l'exécution**.

   ![Replace Lambda function ARN](/static/img/module-8/error-handling-state-machine-retry.png)

4. Maintenant, implémentez un `Retry`. Copiez le code ci-dessous et collez-le en commençant à la ligne 8 entre le nœud `Resource` et le nœud `End`.

```bash
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
```

5. Passez en revue les paramètres de gestion des erreurs. Ces paramètres définissent le comportement du `Retry`:

- `ErrorEquals` (Requis)

  > Un tableau non vide de chaînes qui correspondent aux noms d'erreur. Lorsqu'un état signale une erreur, Step Functions analyse les réessayeurs. Lorsque le nom de l'erreur apparaît dans ce tableau, il met en œuvre la stratégie de nouvelle tentative décrite dans ce réessayeur.

- `IntervalSeconds` (Facultatif)

  > Un nombre entier qui représente le nombre de secondes avant la première nouvelle tentative (1 par défaut). `IntervalSeconds` a une valeur maximale de 99999999.

- `MaxAttempts` (Facultatif)

  > Un nombre entier positif qui représente le nombre maximum de nouvelles tentatives (3 par défaut). Si l'erreur se produit un nombre de fois supérieur à la valeur spécifiée, les nouvelles tentatives cessent et la gestion normale des erreurs reprend. Une valeur de 0 spécifie que l'erreur ou les erreurs ne sont jamais réessayées. `MaxAttempts` a une valeur maximale de 99999999.

- `BackoffRate` (Facultatif)

  > Le multiplicateur par lequel l'intervalle de nouvelle tentative (`IntervalSeconds`) augmente après chaque nouvelle tentative. (2.0 par défaut).

Consultez la documentation pour plus d'informations sur [les paramètres de gestion d'erreurs](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-error-handling.html).

6. Cliquez sur `Enregistrer` puis sur **Démarrer une exécution**. Acceptez l'entrée par défaut et cliquez à nouveau sur **Démarrer une exécution**.

7. Pour afficher votre message d'erreur personnalisé, sélectionnez `StartExecution` dans le volet `Affichage du graphique` et examinez l'onglet `Entrée et sortie`

   ![Failure using Retry output](/static/img-fr/module-8/error-handling-custom-error-retry-output.png)

8. Faites défiler l'écran vers le bas et consultez le tableau `Événements` pour obtenir plus de détails sur l'exécution. Notez les tentatives dans l'historique des événements.
   ![Failure using Retry event history](/static/img-fr/module-8/error-handling-custom-error-retry-event-history.png)

### Vous avez un problème ?

Votre définition ASL doit être similaire à l'extrait ci-dessous. N'oubliez pas de remplacer l'ARN de la fonction Lambda dans le nœud `Resource`.

```bash
{
  "Comment": "A state machine calling an AWS Lambda function with Retry",
  "StartAt": "StartExecution",
  "States": {
    "StartExecution": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:FailFunction",
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "End": true
    }
  }
}
```

Lorsque vous êtes prêt, vous pouvez passer à la page suivante.