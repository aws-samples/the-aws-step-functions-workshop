---
title: 'Módulo 2 - Request Response'
weight: 40
---

Quando o Step Functions chama outro serviço usando estado `Task`, o modelo padrão é [Request Response](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-default). Com esse padrão de integração de tarefas, o Step Functions chamará o serviço e prosseguirá imediatamente para o próximo estado. O estado `Task` não vai aguardar para que o job subjacente seja concluído.

Neste módulo você irá executar uma `Task` usando o padrão Request Response.

**Duração estimada: 15 minutos**
