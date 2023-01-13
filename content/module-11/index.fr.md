---
title: 'Module 11 - Déployer avec AWS SAM'
weight: 130
---

Le [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/) est un framework open source pour la création d'applications serverless. Il fournit une syntaxe abrégée pour definir les fonctions, les APIs, les bases de données et les Event Source Mappings. Avec seulement quelques lignes par ressource, vous pouvez définir l'application que vous souhaitez et la modéliser à l'aide du language YAML. Lors du déploiement, SAM transforme la syntaxe SAM en syntaxe [AWS CloudFormation](https://aws.amazon.com/cloudformation/), ce qui vous permet de créer plus rapidement des applications serverless.

Dans ce module, vous utiliserez AWS SAM pour déployer une application qui configure API Gateway pour déclencher un workflow Step Functions Express synchrone.

**Durée estimée : 30 minutes**