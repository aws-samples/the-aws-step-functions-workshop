---
title: 'Ejecutar flujo de trabajo inicial'
weight: 63
---

Navega a [Step Functions en la consola](https://console.aws.amazon.com/states/home) y haz clic en la máquina de estado que comienza con **"WaitForCallbackStateMachine"**. La arquitectura de la aplicación para este módulo se muestra en el diagrama a continuación. Esta máquina de estado envía un mensaje a SQS utilizando **Wait for Callback** y pasa un token de tarea. SQS luego envía el mensaje y el token a una función Lambda. Sin embargo, la devolución de llamada (paso #3 en el diagrama a continuación) aún no está implementada en la función Lambda. 

![Module 4 architecture](/static/img/module-4/callback-architecture.png)

Ejecuta la máquina de estado ahora utilizando la entrada predeterminada. Observa que la ejecución se detendrá de forma indefinida en el estado `Start Task and Wait For Callback`.

![Module 4 Workflow](/static/img/module-4/initial-workflow.png)

