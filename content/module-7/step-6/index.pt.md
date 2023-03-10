---
title: 'Processar uma execução síncrona através do API Gateway'
weight: 96
---

## Torne a integração síncrona

1. Navegue para o console do API Gateway e selecione a API criada para esse módulo.
   ![API Console](/static/img/module-7/api-console-4.png)
2. Da lista de recursos, ache o recurso `execution` e clique em `POST`.
   ![API Execution](/static/img/module-7/pt-br/api-execution-new.png)
3. Clique em `Solicitação de integração`.
4. Edite a `Ação` clicando no ícone do lápis cinza, mude-a para `StartSyncExecution` e clique no botão de update (sinal de verificação cinza).
   ![API Execution Sync](/static/img/module-7/pt-br/api-integration-setup-sync.png)
5. Teste sua API de novo.
6. Você notará um `Corpo da resposta` com mais detalhes da execução da máquina de estado, incluindo o `input` (entrada) e o `output` (saída).
   ![API Test Result Sync](/static/img/module-7/pt-br/api-test-result-sync.png)

::alert[**Parabéns!** Você acabou de executar um integração síncrona entre o API Gateway e o Step Functions.]{type="success"}
