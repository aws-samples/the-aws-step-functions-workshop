---
title: 'Module 5 - État Choice et état Map'
weight: 70
---

## État de choix
Un état [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) ajoute une logique de branchement à une machine à états. Outre la plupart des champs d'état courants, les états `Choice` contiennent les champs supplémentaires suivants :

- Choix (requis) - un tableau de règles de choix qui détermine l'état vers lequel la machine à états passe ensuite.

- Par défaut (Facultatif, Recommandé) - le nom de l'état vers lequel effectuer la transition si aucune des transitions dans Choices n'est effectuée.

## État Map
Si une charge de travail a un nombre inconnu de branches, l'état [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) peut exécuter un ensemble d'étapes parallèles pour chaque élément d'un tableau. Pour configurer un état `Map`, vous définissez un `Iterator`, qui est un sous-workflow complet. Lorsqu'une exécution Step Functions entre dans un état `Map`, elle itère sur un tableau JSON fournit en parametre d'entrée de l'état. Pour chaque élément, l'état `Map` exécutera un sous-workflow, potentiellement en parallèle. Lorsque toutes les exécutions de sous-workflows sont terminées, l'état `Map` renverra un tableau contenant la sortie de chaque élément traité par l'itérateur.

**Durée estimée : 20 minutes**