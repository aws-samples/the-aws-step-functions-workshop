---
title: 'Módulo 8 - Tratamento de Erros'
weight: 100
---
Qualquer estado pode encontrar erros de execução. Erros podem ocorrer por vários motivos:

- Falhas nas definições das máquinas de estado (por exemplo, estado Choice sem regra de comparação)

- Falhas em execução de tarefas (por exemplo, uma exceção na função Lambda)

- Problemas temporários (por exemplo, falhas de comunicação de redes)

Por padrão, quando um estado reporta um erro a Step Functions causa falha na execução do fluxo de trabalho por inteiro. Entretanto, o Step Functions possui funcionalidades de tratamento de erros que lhe permitem fazer retentativas ou pegar o erro que causou a falha. as funcionalidades de tratamento de erros podem definir procedimentos de retentativas ou pegar e tratar o erro com uma variedade de condições.

Este módulo demonstra o **tratamento de erros** usando função Lambda para simular erros que serão tratados usando os campos `Retry` e `Catch`. 

Revisando a documentação:
- [Tratamento de erro em Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html)
- [Tratamento de erro em AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html)

**Duraçao estimada: 20 minutos**