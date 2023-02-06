---
title: 'Surveiller les exécutions avec Amazon CloudWatch Metrics'
weight: 143

---

La surveillance des métriques est importante pour maintenir la fiabilité, la disponibilité et les performances de vos workflows.

Cet atelier déploie une machine à états appelée `DetectSentimentStateMachine` et quelques autres ressources.

   ![DetectSentiment State Machine](/static/img/module-12/state-machine.png)

Cette machine à états accepte une chaîne de texte en entrée, détecte le sentiment du texte et enregistre le résultat de l'analyse dans une table Amazon DynamoDB. Le workflow appelle une fonction Lambda qui appelle Amazon Comprehend pour effectuer l'analyse des sentiments. Cette machine à états est déclenchée une fois par minute par une règle Amazon EventBridge.

Dans cet exercice, vous utiliserez CloudWatch Metrics pour surveiller les exécutions du workflow `DetectSentimentStateMachine`.

Les métriques Step Functions suivantes de type `Executions` sont disponibles dans CloudWatch 
- ExecutionTime	
- ExecutionThrottled
- ExecutionsAborted	
- ExecutionsFailed	
- ExecutionsStarted	
- ExecutionsSucceeded	
- ExecutionsTimedOut

Plus de détails sur ces mesures peuvent être trouvés [ici](https://docs.aws.amazon.com/step-functions/latest/dg/procedure-cw-metrics.html#cloudwatch-step-functions-execution-metrics).

1. Accédez à la [console CloudWatch](https://console.aws.amazon.com/cloudwatch/home) dans votre console AWS. Assurez-vous d'être dans la bonne région.

2. Sous `Métriques` dans le menu de navigation de gauche, cliquez sur **Toutes les métriques**. Recherchez la zone de statistiques intitulée **États** et cliquez dessus.

   ![CW All Metrics States](/static/img-fr/module-12/cw-all-metrics-states.png)

3. Clicquez **Métriques d'exécution**.

   ![Métriques d'exécution](/static/img-fr/module-12/cw-states-execution-metrics.png)

4. Sélectionnez toutes les métriques répertoriées pour `DetectSentimentStateMachine`.

   ![DetectSentiment Metrics](/static/img-fr/module-12/cw-detect-sentiment-metrics.png)

5. Cliquez sur l'onglet **Graphique des métriques**. Mettez à jour la colonne `Statistique` de `ExecutionTime` sur **Moyenne** et la `Statistic` pour le reste des métriques sur **Sum**. En haut à droite, changez la légende de Ligne en "Numéro".

   ![Sum and Average](/static/img-fr/module-12/cw-metrics-sum-avg.png)

6. Cliquez sur le crayon d'édition à côté du titre du graphique, saisissez **Métriques d'exécution** et cliquez sur **Appliquer**.

7. En haut à droite, cliquez sur le menu déroulant **Actions** et choisissez **Ajouter au tableau de bord**.

- Dans la page Ajouter au tableau de bord, cliquez sur **Créer**.
- Entrez *DetectSentiment* pour le nom du tableau de bord et cliquez sur **Créer**.
- Pour **type de widget**, sélectionnez Numéro.
- Cliquez sur **Ajouter au tableau de bord**.

   ![CW Metrics](/static/img-fr/module-12/cw-add-dashboard.png)

8. Choisissez **Enregistrer le tableau de bord**.

Vous pouvez maintenant voir les métriques d'exécution pour les fonctions d'étape de la machine à états `DetectSentiment`. Vous remarquerez que certaines exécutions ont échoué, indiquées par les métriques `ExecutionsFailed`.

   ![Dashboard Metrics](/static/img-fr/module-12/cw-dashboard.png)

Dans les modules suivants, vous utiliserez CloudWatch Logs et le traçage X-Ray pour déboguer et identifier la cause première de ces échecs.