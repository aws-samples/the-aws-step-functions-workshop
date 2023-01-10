---
title: 'Visão geral da arquitetura'
weight: 93
---

Esse módulo contém os seguintes recursos:

- Três funções do AWS Lambda
- Um API Gateway
- Uma role do AWS IAM usada para integrar o API Gateway com o Step Functions

Nesse módulo você vai criar um fluxo de trabalho Express que recebe uma array de números inteiros como entrada (input) e, em paralelo, calcula a soma, a média e os maiores e menores valores. A máquina de estado retorna um objeto JSON com as respostas de cada uma das execuções paralelas. 

Depois, você vai configurar uma integração assíncrona do API Gateway com a sua máquina de estado. Você vai executar a máquina de estado através de uma requisição para o API Gateway. Então, você vai modificar a integração para tornar a resposta do Step Functions síncrona. 
![Visual Workflow](/static/img/module-7/visual-workflow.png)


