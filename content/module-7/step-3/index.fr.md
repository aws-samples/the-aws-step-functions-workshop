---
title: "Vue d'ensemble de l'architecture"
weight: 93
---

Ce module contient les ressources suivantes :

- Trois fonctions AWS Lambda
- Une API Gateway
- Un rôle AWS IAM utilisé pour intégrer API Gateway avec Step Functions

Dans ce module, vous allez créer un workflow Express qui reçoit un tableau d'entiers en entrée et calcule en parallèle la somme, la moyenne et les valeurs maximale et minimale. La machine à états renvoie un objet JSON avec les réponses de chacune des tâches parallèles.

Ensuite, vous allez configurer une intégration API Gateway asynchrone avec votre machine à états. Vous allez exécuter la machine à états en envoyant une requête à API Gateway. Vous modifierez ensuite l'intégration pour rendre la réponse de Step Functions synchrone.

![Workflow visuel](/static/img/module-7/visual-workflow.png)


