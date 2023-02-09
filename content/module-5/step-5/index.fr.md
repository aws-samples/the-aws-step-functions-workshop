---
title: "Exécuter la machine à états et examiner les résultats"
weight: 75
---

1. Dans la console [Step Functions](https://console.aws.amazon.com/states/home), accédez à **MapStateMachine** et cliquez sur **Démarrer une exécution**. Vous devrez remplacer la charge utile d'exécution par défaut. Agrandissez `Entrée d'exécution` ci-dessous, puis copiez/collez le JSON comme entrée d'exécution.
   ::::expand{header="Entrée d'exécution (Cliquez pour agrandir)" defaultExpanded=false}
   :::code{showCopyAction=true showLineNumbers=false language=json}
   {
      "Data": [
         {
         "orderId": "1",
         "customerId": "1",
         "priority": "HIGH"
         },
         {
         "orderId": "2",
         "customerId": "2",
         "priority": "HIGH"
         },
         {
         "orderId": "3",
         "customerId": "3",
         "priority": "HIGH"
         },
         {
         "orderId": "4",
         "customerId": "4",
         "priority": "LOW"
         },
         {
         "orderId": "5",
         "customerId": "5",
         "priority": "HIGH"
         },
         {
         "orderId": "6",
         "customerId": "6",
         "priority": "LOW"
         },
         {
         "orderId": "7",
         "customerId": "7",
         "priority": "HIGH"
         }
      ]
   }
   ::::


2. L'exécution devrait se terminer en quelques secondes. Une fois l'exécution terminée, parcourez les itérations de l'état `Map` dans la **Vue Table**.
   1. Cliquez sur le symbole gris `+` pour développer les itérations de l'état `Map`.
   2. Ouvrir les itérations #0 à #2, #4 et #6 de l'état `Map` montre que la machine à état a suivi le chemin des éléments de priorité "HIGH", en insérant les détails de la commande pour ces éléments dans le tableau d'entrée dans DynamoDB.
   3. Ouvrir les itérations #3 et #5 de l'état `Map` montre que la machine à état a suivi la logique pour les éléments de priorité "LOW", qui est un état `Success`, détectant que l'élément était un élément de priorité "LOW".
   4. La simultanéité maximale par défaut pour l'état Map est d'une itération à la fois, ce qui signifie que nous traitons le tableau de manière séquentielle. Juste après la fin de la première itération de l'état Map, la seconde commence, et ainsi de suite. Vous pouvez voir les détails des durées et des horodatages des itérations dans les colonnes "Durée", "Chronologie" et "Demarré après". Dans cette exécution, vous verrez comment chaque itération de l'état `Map` a commencé après la fin de la précédente. Dans l'étape suivante, nous montrerons comment mettre à jour votre machine à état pour exécuter plusieurs itérations en parallèle.
   5. Vous pouvez également vérifier la table [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) pour voir si les éléments ont été placés avec succès dans **MapStateTable**.

![Table View avec 1 branche](/static/img-fr/module-5/table-view-1-branch.png)

::alert[**Félicitations !** Vous avez appris à utiliser les états Map et Choice dans une machine à états !]{type="success"}
