---
title: 'Module 8 - Gestion des erreurs'
weight: 100
---
Tout état peut rencontrer des erreurs d'exécution. Des erreurs peuvent survenir pour diverses raisons :

- Problèmes de définition de la machine à états (par exemple, aucune règle correspondante dans un état `Choice`)

- Échecs de tâche (par exemple, une exception dans une fonction Lambda)

- Problèmes transitoires (par exemple, un problème réseau)

Par défaut, lorsqu'un état signale une erreur, Step Functions provoque l'échec complet de l'exécution. Cependant, Step Functions dispose de fonctionnalités de gestion des erreurs qui vous permettent de réessayer ou de détecter les états qui échouent. Les fonctionnalités de gestion des erreurs permettent de définir les conditions de nouvelle tentative et également d'intercepter et gérer divers cas d'erreur.

Ce module illustre la **gestion des erreurs** en utilisant des fonctions Lambda pour simuler des erreurs qui sont gérées à l'aide des champs `Retry` et `Catch`.

Documentation :
- [Gestion des erreurs dans Step Functions](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-error-handling.html)
- [Gestion des erreurs dans AWS Lambda](https://docs.aws.amazon.com/fr_fr/lambda/latest/dg/invocation-retries.html)

**Durée estimée : 20 minutes**