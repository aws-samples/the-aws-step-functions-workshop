---
title: "Exécuter la machine à états et examiner les résultats"
weight: 75
---

1. **S'abonner à la rubrique Amazon SNS (facultatif)**

   - Ouvrez la [console Amazon SNS](https://console.aws.amazon.com/sns/home).

   - Cliquez pour voir les rubriques

   - Cliquez sur le sujet **MapStateTopicforMessages**

   - Sous `Abonnements`, choisissez **Créer un abonnement**.

   - La page `Créer un abonnement` s'affiche, répertoriant l'ARN de rubrique pour la rubrique.

   - Sous `Protocole`, choisissez **Adresse de messagerie**.

   - Sous `Endpoint`, saisissez votre adresse e-mail.

   - Choisissez **Créer un abonnement**.

   - Ouvrez la confirmation d'abonnement envoyée à votre adresse e-mail et cliquez sur le lien **Confirmer l'abonnement**.

:::alert{header="Note" type="warning"}
Vous devez confirmer l'abonnement en cliquant sur le lien envoyé par e-mail avant que l'abonnement ne soit actif.
:::

![SNS](/static/img-fr/module-5/sns-subscription.png)

2. **Ajouter des messages à la file d'attente Amazon SQS**

   - Ouvrez la [console Amazon SQS](https://console.aws.amazon.com/sqs/home).

   - Cliquez sur la file d'attente `MapStateQueueforMessages`.

   - Cliquez sur le bouton **Envoyer et recevoir des messages**.

   - Dans la fenêtre `Envoyer un message`, saisissez un message et cliquez sur **Envoyer un message**.

   - Continuez à envoyer des messages jusqu'à ce que vous en ayez plusieurs dans la file d'attente.

![SQS](/static/img-fr/module-5/sqs-send-message.png)

3. Revenir à [Step Functions](https://console.aws.amazon.com/states/home). Cliquez sur **MapStateMachine**, puis **Démarrer l'exécution**. Copiez/collez le JSON ci-dessous comme valeur d'entrée.
   :::code{showCopyAction=true showLineNumbers=false language=json}
   { "Comment": "Tester les états Map et Choice" }
   :::

4. Lorsqu'une exécution est terminée, sélectionnez certains états dans `Affichage du graphique` et affichez leurs valeurs **Entrée** et **Sortie**. Si vous avez créé un abonnement par e-mail, vous devriez recevoir des e-mails. Vous pouvez également vérifier la table [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) pour voir si les éléments ont été insérés avec succès dans `MapStateTable`.

![DDB](/static/img-fr/module-5/ddb-map-state.png)

::alert[**Félicitations !** Vous avez exécuté une machine à états en utilisant les états Map et Choice.]{type="success"}
