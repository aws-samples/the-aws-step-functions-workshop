---
title: Módulo 4 - Esperar una devolución de llamada con el token de tarea
weight: 60
---

La función [Wait for Callback](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-wait-token) proporciona una forma de pausar un flujo de trabajo de forma indefinida hasta que se devuelve un token de tarea.

Por ejemplo, una tarea podría requerir una aprobación humana, integrarse con un tercero o llamar a un sistema legado. Para flujos de trabajo como estos, una tarea puede pasar un token único a la integración de servicios y pausar. La tarea solo continuará cuando reciba el token de tarea de vuelta con una llamada `SendTaskSuccess` o `SendTaskFailure`. [Integraciones optimizadas para Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html) muestra una lista de los servicios integrados que admiten Esperar devolución de llamada (.waitForTaskToken).

En este módulo implementará un patrón de integración de servicios **Wait for Callback**.

**Duración estimada: 15 minutos**

