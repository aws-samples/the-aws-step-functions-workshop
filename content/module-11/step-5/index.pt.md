---
title: 'Testando o Projeto'
weight: 135
---

Depois de criar sua API REST do API Gateway com Máquina de Estados Espresso Síncrona como a integração de back-end, você pode testar o API Gateway.

### Teste o API Gateway implementado usando o console do API Gateway
1. Abra o [console do Amazon API Gateway](https://console.aws.amazon.com/apigateway/) e faça login.
2. Escolha sua API REST chamada, `SAMStepFunctionsRestApi`.
3. No painel **Recursos**, você pode selecionar o método que deseja testar. Clique no método `POST`.
   ![API Gateway POST](/static/img/module-11/api-gateway-testing.png)
4. No painel **Execução de método**, na caixa **Cliente**, escolha **TESTE**.
5. Copie/cole o JSON abaixo no campo **Corpo da solicitação**.
:::code{showCopyAction=true showLineNumbers=true language=json}
{
"key": "Hello Step Functions!"
}
:::
6.  Clique em **Teste**. As seguintes informações serão exibidas:

- **Solicitação** é o caminho do recurso que foi chamado para o método.
- **Status** é o código de status HTTP da resposta.
- **Latência** é o tempo entre o recebimento da solicitação do chamador e a resposta retornada.
- **Corpo da resposta** é o corpo da resposta HTTP.
- **Cabeçalhos de resposta** são os cabeçalhos de resposta HTTP.
- **Logs**  são as entradas simuladas do Amazon CloudWatch Logs que teriam sido gravadas se esse método fosse chamado fora do console do API Gateway.
  ::alert[Embora as entradas do CloudWatch Logs sejam simuladas, os resultados da chamada do método são reais.]{header="Note"}

A saída do **Corpo da resposta** deve ser:

```bash
"Hello back to you!"
```

### Teste a API Implementada usando cURL

- Abra uma nova janela de terminal em seu ambiente AWS Cloud9.
- Copie o seguinte comando cURL e cole-o na janela do terminal, substituindo `<api-id>` pelo ID da API da sua API e `<region>` pela região onde sua API está implantada. Você pode ter copiado esse URL da saída do CloudFormation na última etapa. Você também pode encontrar o URL de invocação completo no console do API Gateway navegando até **Stages > dev**.

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
