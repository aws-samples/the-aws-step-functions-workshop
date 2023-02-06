---
title: 'Module 10 - Deploiement avec le AWS CDK'
weight: 120
---

Le [AWS Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/v2/guide/home.html) vous permet de créer des applications dans le cloud avec la puissance d'un langage de programmation. Le CDK AWS prend en charge TypeScript, JavaScript, Python, Java, C#/.Net et Go. Les développeurs peuvent utiliser l'un de ces langages de programmation pour définir des composants cloud réutilisables appelés [Constructs](https://docs.aws.amazon.com/cdk/v2/guide/constructs.html). Vous les assemblez ensemble dans des [Stacks](https://docs.aws.amazon.com/cdk/v2/guide/stacks.html) et des [Apps](https://docs.aws.amazon.com/cdk/v2/guide/apps.html).

![AWS CDK diagram](/static/img/module-10/AppStacks.png)

Dans ce module, vous utiliserez AWS CDK avec TypeScript pour déployer une application qui configure API Gateway pour déclencher un workflow Step Functions Express synchrone.

**Durée estimée : 30 minutes**