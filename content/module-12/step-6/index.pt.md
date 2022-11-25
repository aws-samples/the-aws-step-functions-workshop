---
title: 'Corrija os erros e verifique o Rastreamento no X-Ray'
weight: 146
---

## Atualize as unidades de capacidade provisionadas do DynamoDB

1. Navegue até [DynamoDB console](https://console.aws.amazon.com/dynamodbv2/home). Verifique se você está na região correta.

2. Clique em **Tables** no menu à esquerda.

3. Clique na **sentiment-table** no painel central.

4. Na guia Configurações adicionais, clique em **Edit**.

5. Na página Editar capacidade de leitura/gravação, atualize as unidades de capacidade provisionadas em **Write capacity** para **10**

![Update DDB](/static/img/module-12/ddb-wcu.png)

:::alert{header="Important" type="warning"}
A alteração das unidades de capacidade provisionadas na tabela do Amazon DynamoDB pode gerar custos adicionais. Consulte os [preços do Amazon DynamoDB](https://aws.amazon.com/dynamodb/pricing/) para obter a capacidade provisionada. Forneceremos instruções para excluir esses recursos no final deste módulo.
:::

6. Clique **Save changes**.

Aguarde alguns minutos até que as novas configurações de capacidade sejam atualizadas com sucesso.
   
   ![Updated DDB](/static/img/module-12/ddb-updated.png)

## Verifique a correção com X-Ray

1. Navegue para [X-Ray](https://console.aws.amazon.com/xray/home) console para verificar os aceleradores.

2. Atualize o prazo para 1 min.

   ![No throttles](/static/img/module-12/x-ray-update-time.png)

Você deve ver agora que não há mais falhas ou aceleradores.

   ![No throttles](/static/img/module-12/x-ray-no-throttles.png)

Se você verificar as métricas do CloudWatch para as execuções do Step Functions, também verá que o ExecutionsFailed caiu para 0.

   ![Zero Failed executions](/static/img/module-12/cw-states-execution-metrics-0.png)

   ::alert[Parabéns! Você concluiu com sucesso o módulo Observabilidade.]{type="success"}
