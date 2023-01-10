---
title: "Augmentez la simultanéité de l'état Map et exécutez à nouveau le workflow"
weight: 76
---

1. Cliquez sur **Modifier la machine d'état** dans le coin supérieur droit.
![EDIT](/static/img/module-5/edit-state-machine.png)

2. Ouvrez **MapStateStateMachine** dans Workflow Studio en cliquant sur le bouton Workflow Studio sur le côté droit de l'écran.
![EDIT](/static/img/module-5/workflow-studio-button.png)

Si vous voyez l'écran suivant, vous êtes au bon endroit.

![EDIT](/static/img-fr/module-5/module5-workflowstudio.png)

3. Mettez à jour la machine d'état pour augmenter la valeur de simultanéité maximale pour l'état Map. Agrandissez la capture d'écran ci-dessous pour voir comment mettre à jour le paramètre ou suivez les instructions ci-dessous.
   1. Cliquez sur l'état Map dans le canevas de Workflow Studio.
   2. Faites défiler l'onglet Configuration jusqu'à ce que vous voyiez le paramètre "Nombre maximal de simultanéités".
   3. Mettez à jour la valeur sur 2 itérations parallèles.
   4. Cela signifie que notre état Map traitera jusqu'à 2 éléments du tableau d'entrée en parallèle. L'augmentation du nombre d'itérations parallèles nous permet de traiter des ensembles de données plus volumineux en moins de temps par rapport au traitement séquentiel de chaque élément.
   5. Enregistrez vos modifications dans la machine d'état à l'aide du bouton "Appliquer et quitter".

::::expand{header="Panneau de configuration de l'état Map (Cliquez pour agrandir)" defaultExpanded=false}
![EDIT](/static/img-fr/module-5/map-state-configuration-parallel.png)
::::

1. Démarrez une nouvelle exécution de la machine d'état avec la valeur d'entrée que l'exécution précédente.

   ::::expand{header="Valeur d'entrée (Cliquez pour agrandir)" defaultExpanded=false}
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
   :::
   ::::

2. L'exécution devrait se terminer en quelques secondes. Une fois l'exécution terminée, parcourez les itérations de l'état `Map` dans la **Vue Table**.
   1. Les itérations auront les mêmes résultats de traitement pour les éléments `HIGH` vs `LOW`.
   2. Nous pouvons voir nos itérations parallèles en action en affichant les colonnes Chronologie et Démarré après.
   3. L'itération 0 et l'itération 1 ont démarré en même temps.
   4. Une fois l'itération 0 terminée, l'itération 2 a commencé. L'état `Map` crée de nouvelles branches de *workflows* à chaque fois qu'un *workflow* précédent se termine, sans attendre la fin des éxecutions en cours. Même si l'itération 1 n'est pas terminée, l'état Map a commencé à l'itération 2.
   5. Une fois l'itération 1 terminée, l'itération 3 a commencé.
   6. L'itération #3 n'a pas abouti à l'insertion d'un élément dans DynamoDB, la durée a donc été très courte.
   7. Une fois l'itération #3 terminée, l'itération #4 a commencé.

En termes de temps de traitement total, cette exécution a pris environ la moitié de la durée de l'exécution avec seulement 1 itération parallèle. En effet, Step Functions n'était pas limité au traitement d'un élément à la fois et attendait que chaque itération avec des éléments de priorité "HIGH" termine l'écriture dans DynamoDB avant de commencer l'élément suivant.

![Table View avec 2 Branches Parallelles](/static/img-fr/module-5/table-view-2-parallel.png)

::alert[**Félicitations !** Vous avez découvert l'état Map pour augmenter la vitesse de traitement de vos données.]{type="success"}
