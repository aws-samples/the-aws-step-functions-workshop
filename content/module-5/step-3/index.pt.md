---
title: 'Visão geral da arquitetura'
weight: 73
---

Este módulo demonstrará paralelismo dinâmico usando os estados Choice e Map. Este módulo contém os recursos abaixo:

- Uma tabela Amazon DynamoDB

- Uma máquina de estado AWS Step Functions

Neste módulo você passará uma lista de ordenns através de um array em um JSON para ser prcessado pela máquina de estados. O estado Map será usado para fazer a iteração no array, similar a um loop de repetições existentes em linguagens de programação. Em cada iteração o estado Map dinamicamente cria novos fluxos de trabalhos separados. Um estado Choice é usado para determinar qual ação deverá ser executada para cada item do array no JSON, similiar a um IF existente em linguagens de programação. Se o campo `priority` do item tiver um valor `"HIGH"` o Step Functions escreverá os detalhes da ordem no DynamoDB. Se o campo `priority` do item tiver um valor `"LOW"`, nenhuma ação será executada.

![Visual Workflow](/static/img/module-5/visual-workflow.png)

Aprenda mais sobre [integrações com serviços do Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
