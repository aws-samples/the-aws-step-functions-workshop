---
title: 'Revisar el flujo de trabajo'
weight: 32
---

Navega hacia [Step Functions en la consola](https://console.aws.amazon.com/states/home) y clickea en la máquina de estado que comienza por **"TimerStateMachine"**. En este ejemplo ejecutaremos una tarea después de esperar un intervalo de tiempo definido. Clickea **Edit**, y luego clickea en el botón de Workflow Studio:

![Workflow Studio Button](/static/img/module-1/workflow-studio.png)

Revisa la definición en Workflow Studio:

![Module 1 Workflow](/static/img/module-1/workflow.png)

La máquina de estado fue definida usando Amazon States Language (ASL). Clickea en el botón Definition para ver el código ASL. Puedes ver que el código ASL contiene un estado de tipo "Wait".

![Module 1 Code](/static/img/module-1/code.png)
