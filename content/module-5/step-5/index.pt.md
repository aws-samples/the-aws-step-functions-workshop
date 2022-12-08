---
title: 'Execute a máquina de estados e revise os resultados'
weight: 75
---

1. **SAssine um tópico Amazon SNS (opcional)**

   - Abra o [console Amazon SNS](https://console.aws.amazon.com/sns/home).

   - Clique em Tópicos 
   
   - Clique no tópico **MapStateTopicforMessages**

   - Abaixo de Assinaturas, clique em Criar assinatura.

   - A página de criação de assinatura é exibida, listando um ARN de tópico desse tópico.

   - Em protocolo, escolha Email.

   - Em Endpoint, insira seu endereço de e-mail.

   - Clique em Criar assinatura.

   - Abra o e-mail de confirmação de assinatura enviado para seu endereço de e-mail e clique no link `Confirm subscription`.

:::alert{header="Note" type="warning"}
Você precisa confirmar a assinatura através do link enviado por e-mail para que ela se torne ativa.
:::

![SNS](/static/img/module-5/sns-subscription.png)

2. **Adicione mensagens na fila do Amazon SQS**

   - Abra o [console Amazon SQS](https://console.aws.amazon.com/sqs/home).

   - Clique na fila **MapStateQueueforMessages**.

   - Clique no botão **Enviar e receber mensagens**.

   - Na janela Enviar mensagem, insira uma mensagem e clique em **Enviar Mensagem**.

   - Continue enviando mensagens até que você tenha muitas na fila.

![SQS](/static/img/module-5/sqs-send-message.png)

3. Retorne para [Step Functions](https://console.aws.amazon.com/states/home). Clique em **MapStateMachine** e **Start execution**. Copie/cole o JSON abaixo como seus dados de entrada.
   :::code{showCopyAction=true showLineNumbers=false language=json}
   { "Comentario": "Testando os estados Map & Choice" }
   :::

4. Quando a execução terminar selecione alguns dos estados no **Graph Inspector** e veja seus valores de **Input** e **Output**. Se você criou uma assinatura de e-mail também receberá as mensagens por e-mail. Você também pode verificar a tabela [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) para ver se os itens foram inseridos com sucesso na **MapStateTable**.

![DDB](/static/img/module-5/ddb-map-state.png)

::alert[**Parabéns!** Você executou uma máquina de estados usando os estados Map e Choice.]{type="success"}
