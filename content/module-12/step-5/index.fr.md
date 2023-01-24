---
title: "Déboguer les erreurs d'exécution avec les traces AWS X-Ray"
weight: 145
---

Vous pouvez utiliser AWS X-Ray pour visualiser les intégrations de votre machine à états, pour identifier les goulots d'étranglement et pour dépanner les requêtes ayant échoué. Lorsque votre machine à états envoie des données de trace à X-Ray, X-Ray traite les données pour générer une `Service Map` et des résumés de trace consultables.

Avec X-Ray activé pour votre machine à états, vous pouvez tracer les chemins de vos requêtes, ce qui vous donnera un aperçu visuel détaillé de l'ensemble de votre workflow. Vous pouvez utiliser les `Service Maps` X-Ray pour afficher la latence des requêtes, ainsi que pour tous les services AWS intégrés à X-Ray. Vous pouvez également configurer et personnaliser les règles d'échantillonnage dans X-Ray pour contrôler la fréquence d'enregistrement des requêtes.

Pour en savoir plus, lisez [AWS X-Ray et Step Functions](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-xray-tracing.html).

## Activez le traçage X-Ray sur DetectSentimentStateMachine.

1. Ouvrez la [Console Step Functions](https://console.aws.amazon.com/states/home) dans votre console AWS. Assurez-vous d'être dans la bonne région.

2. Cliquez sur la machine à états **DetectSentimentStateMachine-XXXX**.

3. Cliquez sur **Modifier** en haut de la page.

4. Sous `Suivi` dans la page d'édition, selectionnez **Activer le suivi X-Ray**.

:::alert{header="Important" type="warning"}
Pour suivre les exécutions avec X-Ray, le rôle d'exécution Step Functions doit disposer des autorisations X-Ray. Vous pouvez soit laisser Step Functions créer un nouveau rôle pour vous avec les autorisations nécessaires en sélectionnant `Créer un nouveau rôle` sous `Autorisations`, soit les ajouter manuellement à votre rôle existant. Cela a déjà été fait pour vous.
:::

5. Cliquez sur **Enregistrer** en haut de la page.

6. Accédez à [X-Ray](https://console.aws.amazon.com/xray/home) dans la console AWS.

Attendez quelques minutes jusqu'à ce que la console X-Ray soit chargée avec la `Service Map`. Actualisez la page, si nécessaire. Vous verrez la `Service Map` suivante pour `DetectSentimentStateMachine`.

   ![Service Map](/static/img-fr/module-12/x-ray-service-map.png)

Cette `Service Map` montre que votre machine à états interagit avec AWS Lambda et Amazon DynamoDB. La légende rouge sur DetectSentimentStateMachine indique des défauts. La légende violette sur le nœud sentiment-table indique un goulot d'étranglement.

7. Cliquez sur le nœud **sentiment-table** pour étudier ce goulot d'étranglement.

8. Dans le volet Service details à droite, sélectionnez **Restriction** et cliquez sur **Afficher les traces**

   ![Voir les traces](/static/img-fr/module-12/x-ray-view-traces.png)

9. Dans la page `Traces` sous la liste des traces, cliquez sur l'une des traces.

   ![Liste des Traces](/static/img-fr/module-12/x-ray-traces-list.png)

10. Dans la page des détails de la trace, vous verrez une icône d'erreur sur le segment `AWS::StepFunctions::StateMachine`.

    ![View Traces](/static/img-fr/module-12/x-ray-trace-error.png)

11. Plus bas dans la trace, il y a une erreur à côté du sous-segment `Record Transaction`. Cliquez sur l'icône d'erreur.

    ![View Traces](/static/img-fr/module-12/x-ray-exception.png)

L'erreur est causée par la limitation du débit provisionné pour DynamoDB. Le débit demandé a dépassé le niveau configuré de capacité allouée. Pour résoudre le problème, vous pouvez réduire votre débit demandé en diminuant la fréquence de vos écritures, ou vous pouvez augmenter votre capacité en augmentant vos unités de capacité d'écriture provisionnées ou en modifiant le mode de facturation DynamoDB de `Alloué` à `À la demande`.









