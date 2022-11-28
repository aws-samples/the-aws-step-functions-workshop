---
title: 'Implementar resposta'
weight: 65
---

Navegue até [o serviço Lambda no console](https://console.aws.amazon.com/lambda/home) e encontre a função que possua o nome **CallbackWithTaskToken**. Essa é a função responsável pelo processamento das mensagens do SQS. Você irá modificar essa função para implementar o callback.

Revise o código e veja que a função Lambda recebe o `TaskToken` do SQS e pode retornar ele para a maquina de estado como um parâmetro no método `.sendTaskSuccess`.

Descomente o código indicado na imagem abaixo e clique no botão **Deploy**.

![Module 4 Workflow](/static/img/module-4/lambda.png)


