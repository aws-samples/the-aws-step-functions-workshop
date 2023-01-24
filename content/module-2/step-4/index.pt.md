---
title: 'Iniciando a execução'
weight: 44
---

Agora clique em "Start execution" dessa máquina de estados usando os seguintes valores de entrada:

::code[{ "message": "Welcome to re:Invent!", "timer_seconds": 5 }]{showCopyAction=true language="js"}

Navegue até o histórico de eventos de execução para esta execução. Você notará que o tempo de execução da tarefa Send SNS Message é relativamente rápido. A máquina de estado continua assim que a API de publicação do SNS é chamada.

![Módulo 2 Resultado](/static/img/module-2/results.png)

Neste caso, o `"Send SNS Task"` foi concluído em 120ms. Revise seu próprio histórico de eventos de execução para comparar os resultados.

::alert[**Parabéns!**  Você executou a state machine usando o padrão Request Response.]{type="success"}
