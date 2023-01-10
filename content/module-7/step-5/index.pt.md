---
title: 'Processar uma execução assíncrona através do API Gateway'
weight: 95
---

1. Navegue até o console do API Gateway e selecione a API criada para esse módulo.
   ![API Console](/static/img/module-7/api-console-3.png)
2. Da lista de recursos, ache o recurso `execution` e clique em `POST`
   ![API Execution New](/static/img/module-7/pt-br/api-execution-new.png)
3. Clique em `Teste`
4. Ao final da página você vai ver um campo chamado `Corpo da solicitação`, cole o seguinte texto JSON e substitua o exemplo da `stateMachineArn` com a ARN da sua Máquina de Estado:
:::code{showCopyAction=true language=json}
{
"input": "{\"data\": [20,40,60,10,9]}",
"name": "MyExecution",
"stateMachineArn": "arn:aws:states:us-east-1:123456789012:stateMachine:ParallelProcessingMachine"
}
:::
   ![API Test](/static/img/module-7/pt-br/api-test.png)
5. Clique em `Teste`.  
6. Olhe o `Corpo da resposta`. Observe que ele inclui referências ao `executionArn` e ao `startDate`. Essas respostas são retornadas porque a Máquina de Estado foi executada de forma assíncrona.

   ![API Test Result](/static/img/module-7/pt-br/api-test-result.png)

::alert[**Parabéns!** Você acabou de executar um integração assíncrona entre o API Gateway e o Step Functions.]{type="success"}
