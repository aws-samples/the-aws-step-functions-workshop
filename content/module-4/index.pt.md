---
title: Módulo 4 - Wait for Callback com o Token de tarefa
weight: 60
---

A funcionalidade [Wait for Callback](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-wait-token) permite uma forma de pausar um fluxo de trabalho indefinidamanete até que um token de tarefa seja retornado. 

Por exemplo, uma tarefa pode requerer aprovação humana, integraçao com parceiro externo ou chamar um sistema legado. Para fluxos de trabalho como estes uma tarefa pode passar um token único para integração com outro serviço e pausar a execução. A tarefa só será completada quando receber o token de tarefa de volta com a chamada `SendTaskSuccess` ou `SendTaskFailure`. Para ver a lista de serviços integrados que suportam Wait for Callback (.waitForTaskToken), veja [Otimizando integrações para Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).

Neste módulo você irá implementar uma orquestração de tarefa no padrão **Wait for Callback**.

**Duração estimada: 15 minutos**
