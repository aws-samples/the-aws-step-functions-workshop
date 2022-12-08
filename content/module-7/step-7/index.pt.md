---
title: 'Monitorando Fluxos de Trabalho Express'
weight: 97
---

Para monitorarmos Fluxos de Trabalho Express são necessárias ferramentas diferentes das que usamos para Fluxos de Trabalho Standard. Ao invés de usar as ferramentas do Graph Inspector e do Execution Event History, como normalmente você faria com os Fluxos de Trabalho Standard, com os Fluxos de Trabalho Express como o `ParallelProcessingMachine` você usaria o CloudWatch para monitoramento. 

1. Navegue até o console do Step Functions e selecione o `ParallelProcessingMachine`.
2. Todo o histórico de execução é enviado para o CloudWatch Logs. Use as abas de Monitoring e Logging no console do Step Functions para ganhar visibilidade das execuções dos Fluxos de Trabalho Express.
3. A aba de Monitoring mostra 6 gráficos com métricas do CloudWatch para Execution Errors, Execution Succeeded, Execution Duration, Billed Duration, Billed Memory e Executions Started. 
    ![](/static/img/module-7/express-workflows-metrics.png)
4. Navegue para a aba Logging para ver os logs recentes e as configurações de logging, com um link para o CloudWatch Logs.
    ![](/static/img/module-7/express-workflows-logs.png)
5. Clique para ver o Cloudwatch log group, que terá o histórico detalhado de execuções.

::alert[**Parabéns!** Você acabou de monitorar as execuções do seu Fluxo de Trabalho Express do Step Functions.]{type="success"}