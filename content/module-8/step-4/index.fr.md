---
title: 'Intercepter une erreur avec Catch'
weight: 104
---

Les états `Task`, `Map` et `Parallel` peuvent contenir un champ nommé `Catch`. La valeur de ce champ doit être un tableau d'objets, appelés _receveurs_. Chaque receveur peut être configuré pour intercepter un type d'erreur spécifique. Le format ASL définit un ensemble de chaînes prédéfinies correspondant à des erreurs bien connues, commençant toutes par le préfixe `States.`. Les receveurs peuvent également intercepter des erreurs personnalisées. Chaque receveur peut être configuré pour passer à un état **de secours** spécifique. Chaque état de repli peut implémenter une logique de traitement d'erreur. Les types d'erreur prédéfinis incluent :

- `States.ALL` - correspond à n'importe quelle erreur
- `States.DataLimitExceeded` - un dépassement de quota
- `States.Runtime` - une exception d'exécution qui n'a pas pu être traitée
- `States.HeartbeatTimeout` - un état `Task` n'a pas pu envoyer son statut dans les temps
- `States.Timeout` - un état `Task` qui a expiré
- `States.TaskFailed` - un état `Task` qui a échoué lors de l'exécution
- `States.Permissions` - un état `Task` qui n'avait les permissions requises

Lorsqu'un état comporte à la fois des champs `Retry` et `Catch`, Step Functions utilise d'abord tous les réessayeurs appropriés, et ensuite seulement applique la transition définie par le receveur, si les nouvelles tentatives n'ont pas aboutie.

Lisez la documentation pour plus d'informations sur les [noms d'erreurs](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-error-handling.html).

Dans cet exercice, vous allez configurer une machine à états qui interceptera une erreur personnalisée et une erreur `States.Timeout` à l'aide du champ `Catch`.

### Intercepter une erreur personnalisée

1. Localisez la [fonction Lambda](https://console.aws.amazon.com/lambda/home) `ErrorHandlingCustomErrorFunction`. Copiez l'ARN de la fonction et passez en revue le code. Notez que le code génère une erreur nommée `CustomError`.

   ![La fonction Lambda génère une CustomError](/static/img/module-8/error-handling-lambda-function-custom-error.png)

2. Localisez maintenant la [machine à états](https://console.aws.amazon.com/states/home) `ErrorHandlingStateMachineWithCatch-...`. Cliquez sur son lien et cliquez sur le bouton **Modifier** dans le coin supérieur droit de l'écran.

3. Dans le champ `Resource`, remplacez la valeur actuelle par l'ARN de la fonction Lambda copiée à l'étape 1. Lorsque la machine à états appelle cette fonction, la fonction échouera avec l'erreur `CustomError`.

   ![Remplacez l'ARN de la fonction Lambda](/static/img/module-8/error-handling-state-machine-catch.png)

4. Passez en revue le bloc `Catch` de votre définition ASL. Notez qu'il contient trois receveurs. Le premier receveur est configuré pour intercepter une erreur appelée `CustomError`. Lorsqu'il détecte cette erreur, il passe à l'état de secours `CustomErrorFallback`.

   ![Catch CustomError](/static/img/module-8/error-handling-state-machine-catch-custom-error.png)

5. Cliquez sur `Enregistrer` puis sur **Démarrer une exécution**. Acceptez l'entrée par défaut et cliquez à nouveau sur **Démarrer une exécution**.

6. Accédez à l'onglet `Sortie d'exécution` pour afficher la sortie de votre Workflow. Il doit afficher `This is a fallback from a custom Lambda function exception`.

7. Pour afficher la sortie de l'état de repli, sélectionnez l'état `CustomErrorFallback` dans le volet "Affichage du graphique" et cliquez sur l'onglet `Entrée et sortie`.

   ![Failure using Catch output](/static/img-fr/module-8/error-handling-custom-error-catch-output.png)

8. Faites défiler jusqu'au tableau **Événements** pour obtenir plus de détails.
   ![Failure using Catch event history](/static/img-fr/module-8/error-handling-custom-error-catch-event-history.png)



### Détecter une erreur d'expiration

1. Localisez la [fonction Lambda](https://console.aws.amazon.com/lambda/home)  `ErrorHandlingSleep10Function`. Copiez l'ARN de la fonction et passez en revue le code. Notez que la fonction est configurée pour attendre pendant 10 secondes.

   ![La fonction Lambda attend pendant 10 secondes](/static/img/module-8/error-handling-lambda-sleep10.png)

2. Localisez maintenant la [machine à états](https://console.aws.amazon.com/states/home) `ErrorHandlingStateMachineWithCatch-...`. Cliquez sur son lien et cliquez sur le bouton **Modifier** dans le coin supérieur droit de l'écran.

3. Dans le champ `Resource`, remplacez la valeur actuelle par l'ARN de la fonction Lambda copiée à l'étape 1. Lorsque la machine à états invoque cette fonction, la fonction se met en veille pendant 10 secondes.

   ![Remplacez l'ARN de la fonction Lambda](/static/img/module-8/error-handling-state-machine-catch.png)

4. Notez que le champ `TimeoutSeconds` pour la `Task` est défini sur 5 secondes. Notez le receveur configuré pour intercepter le type d'erreur `States.Timeout`. Ce receveur passe à l'état `TimeoutFallback`.

   ![Passez en revue le receveur](/static/img/module-8/error-handling-state-machine-timeout.png)

5. Cliquez sur `Enregistrer` puis sur **Démarrer l'exécution**. Acceptez l'entrée par défaut et cliquez à nouveau sur **Démarrer l'exécution**.

6. Accédez à l'onglet `Entrée et sortie d'exécution` pour afficher la sortie de votre workflow. Il devrait afficher `This is a fallback from a timeout error`

7. Pour afficher la sortie de l'état de repli, sélectionnez l'état `TimeoutFallback` dans le volet "Affichage du graphique" et cliquez sur l'onglet `Entrée et sortie`.
   ![Catch d'une erreur d'expiration](/static/img-fr/module-8/error-handling-timeout-error-catch-output.png)

8. Faites défiler l'écran jusqu'au tableau `Événements` pour obtenir plus de détails
   ![Historique d'événements](/static/img-fr/module-8/error-handling-timeout-error-catch-event-history.png)

   ::alert[**Félicitations !** Vous avez terminé avec succès le module de gestion des erreurs.]{type="success"}
