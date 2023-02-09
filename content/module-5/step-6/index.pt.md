---
title: 'Aumente a concorrência do estado Map e execute fluxo de trabalho novamente'
weight: 76
---
1. Clique em **Edit State Machine** no canto superior direito.
![EDIT](/static/img/module-5/edit-state-machine.png)

2. Abra o **MapStateStateMachine** no Workflow Studio clicando no botão Workflow Studio no lado direito da tela.
![EDIT](/static/img/module-5/workflow-studio-button.png)

Se você vê a figura abaixo, está no caminho correto.

![EDIT](/static/img/module-5/module5-workflowstudio.png)

3. Atualize a máquina de estado para aumentar a concorrência máxima no estado Map. Expanda o printscreen abaixo para ver como atualizar a configuração ou siga as instruções abaixo.
   1. Clique no estado Map dentro do Workflow Studio.
   2. Na aba Configuration desça até encontrar o campo Maximum concurrency.
   3. Atualize o valor para 2 execuções paralelas.
   4. Isso significa que nossa máquina de estados conseguirá processar 2 items do array por vez. Aumentando o número de execuções paralelas nos permite executar o processamento de grande quantidade dados em um tempo menor do que quando processamos cada item sequencialmente.
   5. Salve as alterações da sua máquina de estado clicando no botão `Apply and exit`.

::::expand{header="Painel de configuração do estado Map (Click to expand)" defaultExpanded=false}
![EDIT](/static/img/module-5/map-state-configuration-parallel.png)
::::

1. Inicia uma nova execução da máquina de estados com o mesmo payload de entrada da execução anterior.

   ::::expand{header="Execution Payload (Click to expand)" defaultExpanded=false}
   :::code{showCopyAction=true showLineNumbers=false language=json}
   {
      "Data": [
         {
         "orderId": "1",
         "customerId": "1",
         "priority": "HIGH"
         },
         {
         "orderId": "2",
         "customerId": "2",
         "priority": "HIGH"
         },
         {
         "orderId": "3",
         "customerId": "3",
         "priority": "HIGH"
         },
         {
         "orderId": "4",
         "customerId": "4",
         "priority": "LOW"
         },
         {
         "orderId": "5",
         "customerId": "5",
         "priority": "HIGH"
         },
         {
         "orderId": "6",
         "customerId": "6",
         "priority": "LOW"
         },
         {
         "orderId": "7",
         "customerId": "7",
         "priority": "HIGH"
         }
      ]
   }
   :::
   ::::

2. A execução deverá terminar em alguns segundos. Quando a execução terminar veja os detalhes da execução em **Table View**.
   1. As iterações deverão ter os mesmos resultados para ambos processamentos para os items `HIGH` e `LOW`.
   2. Voce pode ver nossas iterações paralelas olhando nas colunas Timeline e Started After.
   3. Iteração #0 e Iteração #1 começaram no mesmo momento.
   4. Quando a Iteração #0 terminou a iteração #2 começou. O estado Map criou fluxos de trabalhos separados assim que fluxos de trabalhos anteriores foram concluídos sem esperar que todos os lufxos de trabalhos sendo executados terminassem. Embora  Iteração #1 não tenha terminado, to estado Map começou a Iteração #2.
   5. Quando a Iteração #1 terminou, Iteração #3 começou.
   6. Iteração #3 não inseriur o item no DynamoDB, por isso a duração foi muito curta.
   7. Quando a Iteração #3 terminou, Iteração #4 começou.

Em termos de tempo total de processamento, essa execução teve quase metade do tempo com apenas uma execução em paralelo. Isso é porque o Step Functions não foi restrito a executar uma iteração por vez e esperar cada iteração com item com prioridade `HIGH` terminsasse de inserir o item no DynamoDB antes de começar o próximo item.

![Table View com 2 fluxos de trabalhos paralelos](/static/img/module-5/table-view-2-parallel.png)

::alert[**Parabéns!** Você também aproveitou as configurações de concorrência máxima para aumentar a velocidade de processamento!.]{type="success"}

