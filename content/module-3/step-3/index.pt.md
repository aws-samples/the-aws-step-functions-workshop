---
title: 'Executar tarefa assíncrona'
weight: 53
---

Navegue até [Step Functions in the console](https://console.aws.amazon.com/states/home) e clique na máquina de estado que começa com **"BatchJobNotification"**. Este fluxo de trabalho envia um trabalho do AWS Batch. Em seu estado inicial, o trabalho é assíncrono. A máquina de estado envia o trabalho para o serviço AWS Batch, mas não espera a conclusão do trabalho. Em vez disso, ele passa imediatamente para o próximo estado e envia uma mensagem Notify Success para um tópico do Amazon SNS.

Aqui está a aparência do fluxo de trabalho inicial:

![Module 3 Workflow](/static/img/module-3/initial-workflow.png)

Aqui está a aparência da definição de tarefa para o trabalho do AWS Batch. Veja a chave Resource.

![Module 3 Code](/static/img/module-3/initial-code.png)

Agora clique em **Iniciar execução** e use a entrada padrão. O serviço AWS Batch executa um trabalho, que pode levar um minuto ou mais para ser concluído. Observe a rapidez com que essa execução é concluída.

![Initial graph](/static/img/module-3/initial-graph.png)

Agora imagine que precisamos que nossa máquina de estado permaneça sincronizada com o AWS Batch e continue apenas quando o trabalho for concluído.