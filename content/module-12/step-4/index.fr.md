---
title: "Enregistrer l'historique d'exécution avec Amazon CloudWatch Logs"
weight: 144
---

Les workflows standards enregistrent l'historique d'exécution dans AWS Step Functions, et vous pouvez éventuellement configurer la journalisation dans Amazon CloudWatch Logs.
Lorsque vous créez un workflow standard, il ne sera pas configuré pour activer la journalisation dans CloudWatch Logs par défaut. Pour configurer la journalisation, vous pouvez passer le paramètre `LoggingConfiguration` lorsque vous utilisez les APIs `CreateStateMachine` ou `UpdateStateMachine`.
CloudWatch Logs offre plusieurs avantages à l'analyse des fichiers de logs par rapport à la journalisation par défaut, notamment la possibilité d'analyser davantage vos données à l'aide de CloudWatch Logs Insights.

Pour plus d'informations, lisez [Analyse des données de journaux avec CloudWatch Logs Insights](https://docs.aws.amazon.com/fr_fr/AmazonCloudWatch/latest/logs/AnalyzingLogData.html). Pour comprendre les stratégies IAM requises pour la journalisation dans CloudWatch Logs, lisez [Politiques IAM pour la journalisation dans les journaux CloudWatch](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/cw-logs.html#cloudwatch-iam-policy).

## Configurer CloudWatch Logs

1. Ouvrez la [Console Step Functions](https://console.aws.amazon.com/states/home) dans votre console AWS. Assurez-vous d'être dans la bonne région.

2. Cliquez sur **Machines d'état** dans le volet de navigation de gauche. Vous verrez la machine à états nommée `DetectSentimentStateMachine-XXXX` déployée pour vous dans le cadre de cet atelier

3. Cliquez sur la machine à états **DetectSentimentStateMachine-XXXX**.

4. Dans la page DetectSentimentStateMachine, cliquez sur l'onglet **Journalisation**. Vous verrez que le niveau de journalisation est `OFF`, ce qui indique que la journalisation CloudWatch n'est pas activée.

   ![CW Log disabled](/static/img-fr/module-12/cw-log-disabled.png)

    Activons la journalisation CloudWatch.

5. Cliquez sur **Modifier** en haut de la page.

6. Dans la page Modifier DetectSentimentStateMachine, faites défiler vers le bas pour modifier le niveau de journalisation sous Journalisation sur **ALL** et laissez le reste par défaut.

   ![CW Log activés](/static/img-fr/module-12/cw-logging-enabled.png)

7. Cliquez sur **Enregistrer** en haut de la page.

Retournez à la page DetectSentimentStateMachine et attendez quelques minutes. Actualisez la page et vous verrez la section `CloudWatch Logs Insights` remplie de journaux.

   ![CW Logs](/static/img-fr/module-12/cw-logs.png)

## Requêtez CloudWatch Logs Insights

1. Ouvrez la [console CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Cliquez sur **Logs Insights** sous Journaux dans le menu de navigation de gauche.

2. Sur la page Logs Insights, sélectionnez le groupe de journaux **/aws/vendedlogs/states/DetectSentimentStateMachine-XXX-Logs**.

   ![CWL Vended](/static/img-fr/module-12/cwl-vendedlogs.png)

3. Dans le champ de texte, copiez-collez la requête suivante et cliquez sur **Exécuter la requête**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, type
| stats count(*) as typeCount by type
| sort typeCount desc
:::

Cette requête CloudWatch Log Insights affiche les statistiques de divers types d'exécution.

   ![CWL query](/static/img-fr/module-12/cwl-query.png)

Faites défiler vers le bas dans la section des résultats pour consulter les résultats complets. Vous verrez les résultats `TaskFailed` et `ExecutionFailed`.

   ![CWL failed](/static/img-fr/module-12/cwl-failed.png)

12. Pour identifier la cause des échecs d'exécution, copiez et collez la requête suivante dans le champ de texte CloudWatch Log Insights et cliquez sur **Exécuter la requête**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, execution_arn, details.error, details.cause
| filter type = 'TaskFailed'
| limit 100
:::

![CWL failureReasons 1](/static/img-fr/module-12/cwl-failureReasons-1.png)

![CWL CWL failureReasons 2](/static/img-fr/module-12/cwl-failureReasons-2.png)

Ces erreurs indiquent que les échecs d'exécution de Step Functions étaient dus à la limitation du débit provisionné par DynamoDB. Dans la section suivante, vous utiliserez le traçage avec X-Ray pour étudier plus en détail ces défaillances.