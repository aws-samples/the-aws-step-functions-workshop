---
title: 'Testando o projeto'
weight: 135
---

Depois de criar sua API REST do API Gateway com Synchronous Express State Machine como a integração de back-end, você pode testar o API Gateway.

### Teste o API Gateway implantado usando o console do API Gateway

1. Abra o [Amazon API Gateway console](https://console.aws.amazon.com/apigateway/) e entre.
2. Escolha sua REST API chamada, `SAMStepFunctionsRestApi`.
3. No painel **Resources** , você pode selecionar o método que deseja testar. Clique no método `POST` .
   ![API Gateway POST](/static/img/module-11/api-gateway-testing.png)
4. No painel **Method Execution** , na caixa **Client** , escolha **TEST**.
5. Copie/Cole o JSON abaixo no campo **Request Body** .
   :::code{showCopyAction=true showLineNumbers=true language=json}
   {
   "key": "Hello Step Functions!"
   }
   :::
6. Clique **Test**. A seguinte informação será mostrada:

- **Request** é o caminho do recurso que foi chamado pelo método.
- **Status** é o código de status da resposta HTTP.
- **Latency** é o tempo entra o recebimento da requisição pelo chamador e a resposta retornada.
- **Response Body** é o corpo da resposta HTTP.
- **Response Headers** são os cabeçalhos na resposta HTTP.
- **Logs** são as entradas de Logs no Amazon CloudWatch que devem ser escritas se esse método foi chamado de fora do console do API Gateway.
  ::alert[Embora as entradas do CloudWatch Logs sejam simuladas, os resultados da chamada do método são reais.]{header="Note"}

A saída do **Response Body** deve ser:

```bash
"Hello back to you!"
```

### Teste a API implantada usando cURL

- Abra uma nova janela de terminal em seu ambiente AWS Cloud9.
- Copie o seguinte comando cURL e cole-o na janela do terminal, substituindo `<api-id>` pelo ID da API de sua API e `<region>` pela região onde sua API está implantada. Você pode ter copiado este URL da saída do CloudFormation na última etapa. Você também pode encontrar o URL de chamada completo no console do API Gateway navegando para **Estágios > dev**.

```bash
curl -X POST\
 'https://<api-id>.execute-api.<region>.amazonaws.com/dev' \
 -d '{"key":"Hello Step Functions"}' \
 -H 'Content-Type: application/json'
```

A saída do **Response Body** deve ser:

```bash
"Hello back to you!"
```

::alert[**Parabéns!** Você concluiu este módulo com sucesso.]{type="success"}
