---
title: 'Descripción general de la arquitectura'
weight: 73
---

Este módulo demuestra el paralelismo dinámico usando estados Map y Choice. Contiene los siguientes recursos:

- Una tabla de Amazon DynamoDB

- Una máquina de estados AWS Step Functions

Es este módulo, pasarás un arreglo JSON de órdenes a ser procesadas por tu máquina de estados. Un estado tipo Map es usado para iterar sobre el arreglo de entrada, similiar a un loop en los lenguajes de programación. En cada iteración, el estado tipo Map dinámicamente crea ramas separadas de flujos de trabajo. Un estado tipo choice es usado para determinar que acción tomar para cada elemento del arreglo JSON, similar a una declaración if en los lenguajes de programación. Si el campo `priority` de los elementos actuales tienen un valor `"HIGH"`, Step Funcitons escribe el detalle de la orden dentro de DynamoDB. Si el campo `priority` del elemento actual es `"LOW"`, ninguna acción será realizada. 

![Visual Workflow](/static/img/module-5/visual-workflow.png)

Obtenga más información sobre [Integraciones de servicios de Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
