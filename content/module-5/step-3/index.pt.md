---
title: 'Visão geral da arquitetura'
weight: 73
---

Este módulo demonstrará paralelismo dinâmico usando os estados Choice e Map. Este módulo contém os recursos abaixo:

- Duas funções AWS Lambda

- Uma fila Amazon Simple Queue Service (Amazon SQS)

- Um tópico Amazon Simple Notification Service (Amazon SNS)

- Uma tabela Amazon DynamoDB

- Uma máquina de estado AWS Step Functions

Neste projeto a Step Function invoca uma função AWS Lambda que obtém mensagens de uma fila Amazon SQS. A função Lambda então retorna um JSON com a lista de mensagens para o estado Map. O estado Map percorre a lista criando dinamicamente um fluxo de trabalho separado para cada item da lista. Cada fluxo de trabalho insere a mensagem no DynamoDB e então invoca uma segunda função Lambda para remover a mensagem da fila do Amazon SQS. No final cada fluxo de trabalho publica a mensagem no tópico Amazon SNS.

![Visual Workflow](/static/img/module-5/visual-workflow.png)

Aprenda mais sobre [integrações com serviços do Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
