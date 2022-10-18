---
title: 'Revisando o fluxo de trabalho'
weight: 43
---

Navegue para o [Step Functions no console](https://console.aws.amazon.com/states/home) e clique na máquina de estado que começa com **"RequestResponseStateMachine"**. Neste aplicativo de exemplo, aguardaremos um delay especificado e, em seguida, publicaremos em um tópico do SNS usando o padrão de Request Response.

Quando você especifica um serviço no campo `"Resource"` do seu estado, e você fornece apenas o recurso, o Step Functions aguardará uma resposta HTTP da API do serviço e, em seguida, avançará imediatamente para o próximo estado. O Step Functions não vai aguardar até que o job seja concluído. Esse padrão é chamado de Request Response.

Revise a definição no Workflow Studio:

![Módulo 2 Workflow](/static/img/module-2/workflow.png)

Veja o campo `"Resource"`do estado abaixo. Esse código designa o padrão de integração de serviços Request Response.

![Módulo 2 Código](/static/img/module-2/code.png)
