---
title: 'Descripción general de la arquitectura'
weight: 73
---

Este módulo demuestra el paralelismo dinámico mediante los estados Map y Choice. Contiene los siguientes recursos:

- Dos funciones de AWS Lambda

- Una cola de Amazon Simple Queue Service (Amazon SQS)

- Un tópico de Amazon Simple Notification Service (Amazon SNS)

- Una tabla de Amazon DynamoDB

- Una máquina de estados AWS Step Functions

En este módulo, Step Functions invoca una función de AWS Lambda que recupera los mensajes de una cola de Amazon SQS. Un estado `Choice` determina la ruta de ejecución de la máquina de estados. Si hay mensajes que procesar, el estado `Choice` pasa una matriz JSON de esos mensajes a un estado `Map`. El estado `Map` recorre cada mensaje de la matriz de forma dinámica y crea ramas de flujo de trabajo independientes. Cada rama del flujo de trabajo escribe un mensaje en DynamoDB y, a continuación, invoca una segunda función de Lambda para eliminar el mensaje de Amazon SQS. Por último, la rama publica el mensaje en el tema Amazon SNS.

![Visual Workflow](/static/img/module-5/visual-workflow.png)

Obtenga más información sobre [Integraciones de servicios de Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html).
