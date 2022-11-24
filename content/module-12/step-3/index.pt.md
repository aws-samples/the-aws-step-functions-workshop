---
title: 'Monitorar execuções com Métricas do Amazon CloudWatch'
weight: 143

---

O monitoramento de métricas é importante para manter a confiabilidade, a disponibilidade e o desempenho de seus fluxos de trabalho.

Este workshop implanta uma máquina de estado chamada *DetectSentimentStateMachine* e alguns outros recursos.

   ![DetectSentiment State Machine](/static/img/module-12/state-machine.png)

Essa máquina de estado aceita uma string de entrada, detecta o sentimento do texto na string e registra o resultado da análise em uma tabela do Amazon DynamoDB. O fluxo de trabalho invoca uma função do Lambda que chama o Amazon Comprehend para realizar a análise de sentimento. Essa máquina de estado é acionada uma vez por minuto por uma regra do Amazon EventBridge.

Neste exercício, você usará as métricas do CloudWatch para monitorar as execuções do fluxo de trabalho *DetectSentimentStateMachine*.

As seguintes métricas de Step Functions Execution estão disponíveis no CloudWatch
- ExecutionTime	
- ExecutionThrottled
- ExecutionsAborted	
- ExecutionsFailed	
- ExecutionsStarted	
- ExecutionsSucceeded	
- ExecutionsTimedOut

Mais detalhes sobre essas métricas podem ser encontrados [aqui](https://docs.aws.amazon.com/step-functions/latest/dg/procedure-cw-metrics.html#cloudwatch-step-functions-execution-metrics).

1. Navegue até o [console do CloudWatch](https://console.aws.amazon.com/cloudwatch/home) em seu console AWS. Verifique se você está na região correta.

2. Em `Metrics` no menu de navegação à esquerda, clique em **All Metrics**. Localize a caixa de métricas denominada **States** e clique nela.

   ![CW All Metrics States](/static/img/module-12/cw-all-metrics-states.png)

3. Clique **Execution Metrics**.

   ![Execution Metrics](/static/img/module-12/cw-states-execution-metrics.png)

4. Selecione todas as métricas listadas para `DetectSentimentStateMachine`. 

   ![DetectSentiment Metrics](/static/img/module-12/cw-detect-sentiment-metrics.png)

5. Clique na guia **Graphed metrics**. Atualize a coluna `Statistic` de `ExecutionTime` para **Average** e a `Statistic` para o restante das métricas para **Sum**. No canto superior direito, altere a legenda de Linha para 'Número'.

   ![Sum and Average](/static/img/module-12/cw-metrics-sum-avg.png)

6. Clique no lápis de edição ao lado do título do gráfico, digite **Execution Metric** e clique em **Apply**.

7. No canto superior direito, clique em **Actions** dropdown e escolha **Add to dashboard**.

- Na página Adicionar ao painel, clique em **Create new**.
- Digite *DetectSentiment* para o nome do painel e clique **Create**.
- Para **widget type**, selecione Number.
- Clique **Add to dashboard**.

   ![CW Metrics](/static/img/module-12/cw-add-dashboard.png)

8. Escolha **Save dashboard**.

Agora você pode ver as métricas de execução para funções de etapa da máquina de estado DetectSentiment. Você notará que há execuções que falharam, indicadas pelas métricas ExecutionsFailed.

   ![Dashboard Metrics](/static/img/module-12/cw-dashboard.png)

Nos próximos módulos, você usará o rastreamento nos logs do CloudWatch e X-Ray para depurar e identificar a causa raiz dessas falhas.