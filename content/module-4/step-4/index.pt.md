---
title: 'Revise as definições do ASL'
weight: 64
---

Revise as definições do ASL para esta máquina de estado. Embora a lógica de callback `.waitForTaskToken` esteja implementada nas definições do ASL, o callback ainda não está sendo executado na função Lambda que processa as mensagens SQS.

![Module 4 Workflow](/static/img/module-4/code.png)
