---
title: 'Módulo 6 - Processamento de Entrada e Saída'
weight: 80
---
Uma execução do Step Functions recebe um texto JSON como entrada e transmite essa entrada para o primeiro estado no fluxo de trabalho. Cada estado recebe JSON como entrada e geralmente passa JSON como saída para o próximo estado. Entender como essas informações fluem de estado para estado, e aprender a filtrar e manipular esses dados, é a chave para efetivamente projetar e implementar fluxos de trabalho no AWS Step Functions. 

No Amazon States Language (Idioma de estados da Amazon) os campos a seguir filtram e controlam o fluxo de JSON de estado para estado: 

- `InputPath`
- `OutputPath`
- `ResultPath`
- `Parameters`
- `ResultSelector`

Leia a documentação para aprender mais sobre [Processamento de Entrada e Saída](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-input-output-filtering.html).

**Duração Estimada: 25 minutos**