---
title: Module 4 - Wait for a Callback with the Task Token
weight: 60
---

O recurso [Wait for Callback](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-wait-token) fornece uma maneira de pausar um fluxo de trabalho indefinidamente até que um token de tarefa seja retornado.

Por exemplo, uma tarefa pode exigir aprovação humana, integrar-se a terceiros ou chamar um sistema legado. Para fluxos de trabalho como esses, uma tarefa pode passar um token único para a integração do serviço e pausar. A tarefa só será retomada quando receber o token da tarefa de volta com uma chamada `SendTaskSuccess` ou `SendTaskFailure`. [Integrações otimizadas para Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html) mostra uma lista dos serviços integrados que suportam Wait for Callback (. waitForTaskToken).

Neste módulo, você implementará um padrão de integração de serviço **Wait for Callback**.

**Duração Estimada: 15 minutos**
