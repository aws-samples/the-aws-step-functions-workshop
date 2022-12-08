---
title: 'Revisar Fluxo de Trabalho'
weight: 32
---

Navegue até [Step Functions no console](https://console.aws.amazon.com/states/home) e clique na máquina de estado que começa com **"TimerStateMachine"**. Neste aplicativo de exemplo, executaremos uma tarefa após aguardar um atraso (delay) especificado. Clique em **Editar** e, em seguida, clique no botão do Workflow Studio:

![Workflow Studio Button](/static/img/module-1/workflow-studio.png)

Revise a definição no Workflow Studio:

![Module 1 Workflow](/static/img/module-1/workflow.png)

A máquina de estado é definida usando Amazon States Language (ASL). Clique no botão Definição para visualizar o código ASL. Você pode ver que o ASL contém um estado "Wait".

![Module 1 Code](/static/img/module-1/code.png)
