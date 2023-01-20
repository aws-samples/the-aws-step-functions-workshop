---
title: 'Corrigez les erreurs et vérifiez les traces X-Ray'
weight: 146
---

## Mettre à jour les unités de capacité provisionnées DynamoDB

1. Accédez à la [console DynamoDB](https://console.aws.amazon.com/dynamodbv2/home). Assurez-vous d'être dans la bonne région.

2. Cliquez sur **Tables** dans le menu de gauche.

3. Cliquez sur **sentiment-table** dans le volet central.

4. Dans l'onglet Paramètres supplémentaires, cliquez sur **Modifier**.

5. Dans la page Modifier la capacité de lecture/écriture, mettez à jour les unités de capacité allouées sous **Capacité d'écriture** sur **10**

![Update DDB](/static/img-fr/module-12/ddb-wcu.png)

:::alert{header="Important" type="warning"}
La modification des unités de capacité allouées sur la table Amazon DynamoDB peut entraîner des coûts supplémentaires. Veuillez consulter la [tarification Amazon DynamoDB](https://aws.amazon.com/dynamodb/pricing/) pour connaître tarification de la capacité allouée. Nous fournirons des instructions pour supprimer ces ressources à la fin de ce module.
:::

6. Cliquez sur **Enregistrer les modifications**.

Attendez quelques minutes jusqu'à ce que les nouveaux paramètres de capacité aient été mis à jour avec succès.

   ![Updated DDB](/static/img-fr/module-12/ddb-updated.png)

## Vérifiez le correctif avec X-Ray

1. Accédez à la console [X-Ray](https://console.aws.amazon.com/xray/home) pour vérifier les restrictions.

2. Mettez à jour le délai à 1 min.

   ![Tout est vert](/static/img-fr/module-12/x-ray-update-time.png)

Vous devriez voir maintenant qu'il n'y a plus de défauts ou de goulot d'étranglement.

   ![Plus de goulot d'étranglement ni d'erreur](/static/img-fr/module-12/x-ray-no-throttles.png)

Si vous vérifiez les métriques CloudWatch pour les exécutions Step Functions, vous devriez également voir ExecutionsFailed passer à 0.

   ![Zero executions en erreur](/static/img/module-12/cw-states-execution-metrics-0.png)

  ::alert[**Félicitations !** Vous avez terminé ce module avec succès.]{type="success"}
