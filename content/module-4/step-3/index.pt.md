---
title: 'Executar fluxo de trabalho inicial'
weight: 63
---

Navegue até [Step Functions no console](https://console.aws.amazon.com/states/home) e clique na máquina de estado que começa com **"WaitForCallbackStateMachine"**. A arquitetura da aplicação que usaremos nesse módulo é exibida no diagrama abaixo. Essa máquina de estado envia mensagens para o SQS usando **Wait for Callback** e passa um token de tarefa. O SQS envia a mensagem e o token de tarefa para a função Lambda. Entretanto, o callback (passo #3 no diagrama abaixo) ainda não está implementado na função Lambda. 

![Module 4 architecture](/static/img/module-4/callback-architecture.png)

Execute a maquina de estado agora usando uma entrada padrão. Veja que a execução ficará parada no estado `Start Task and Wait For Callback` indefinidamente.

![Module 4 Workflow](/static/img/module-4/initial-workflow.png)
