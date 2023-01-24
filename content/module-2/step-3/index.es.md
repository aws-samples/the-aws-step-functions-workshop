---
title: 'Flujo de trabajo de revisión'
weight: 43
---

Navega a [Step Functions en la consola](https://console.aws.amazon.com/states/home) y Haz clic en la máquina de estado que comienza con **"RequestResponseStateMachine"**. En esta aplicación de muestra esperaremos un retraso especificado, luego publicaremos en SNS utilizando el patrón de respuesta de la solicitud.

Step Functions llamará a la API del servicio para el recurso definido (utilizando el campo `resource`) en su estado de tarea. Step Functions esperará una respuesta HTTP de la API del servicio y luego avanzará inmediatamente al siguiente estado. Esto se llama el patrón de respuesta a solicitud.

Si la API del servicio inicia un trabajo asíncrono, Step Functions no esperará que ese trabajo se complete. Puede obtener más información sobre cómo iniciar y verificar los resultados de los trabajos asíncronos más adelante en el taller.

Revisa la definición en Workflow Studio:

![Module 2 Workflow](/static/img/module-2/workflow.png)

Observa el campo `"Resource"` del estado de tarea a continuación. Este código define una integración de servicio utilizando el patrón respuesta de la solicitud.

![Module 2 Code](/static/img/module-2/code.png)

