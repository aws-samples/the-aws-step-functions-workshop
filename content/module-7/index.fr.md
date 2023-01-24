---
title: 'Module 7 - API Gateway, Parallel State, Express workflows'
weight: 90
---
Amazon API Gateway est un service entièrement géré qui permet aux développeurs de créer, publier, maintenir, surveiller et sécuriser facilement des APIs. Step Functions s'intègre directement à API Gateway, vous permettant de déclencher l'exécution d'une machine à états avec une requête HTTP. API Gateway peut être utilisé avec les workflows Standard et Express. Les intégrations peuvent être synchrones ou asynchrones.

L'état `Parallel` peut accélérer le traitement des données en créant un nombre fixe de branches d'exécution parallèles dans votre machine à états.

Dans ce module, vous découvrirez comment API Gateway s'intègre aux workflows Express de façon asynchrone et synchrone. Vous apprendrez également à utiliser l'état `Parallel` pour créer plusieurs branches logiques simultanées.

![Architecture API Gateway vers Step Functions](/static/img/module-7/architecture.png)

En savoir plus sur les [états Parallel](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/amazon-states-language-parallel-state.html).

En savoir plus sur [API Gateway Integration](https://docs.aws.amazon.com/fr_fr/apigateway/latest/developerguide/api-gateway-api-integration-types.html).

**Durée estimée : 25 minutes**