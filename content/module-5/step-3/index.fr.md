---
title: "Vue d'ensemble de l'architecture"
weight: 73
---

Ce module illustre le parallélisme dynamique à l'aide des états Map et Choice. Ce module contient les ressources suivantes :

- Une table Amazon DynamoDB

- Une machine à états AWS Step Functions

Dans ce module, vous allez transmettre un tableau JSON de commandes à traiter par votre machine à état. Un état `Map` est utilisé pour itérer sur le tableau d'entrée, similaire à une boucle dans les langages de programmation. À chaque itération, l'état `Map` crée dynamiquement des branches de workflow distinctes. Un état `Choice` est utilisé pour déterminer quelle action entreprendre pour cet élément dans le tableau JSON, similaire à une instruction `if` dans les langages de programmation. Si le champ `priority` de l'élément actuel a une valeur "HIGH", Step Functions écrit les détails dans DynamoDB. Si le champ `priority` de l'élément actuel est "LOW", aucune action n'est entreprise.

![Workflow visuel](/static/img/module-5/visual-workflow.png)

En savoir plus sur les [intégrations de services Step Functions](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-service-integrations.html).
