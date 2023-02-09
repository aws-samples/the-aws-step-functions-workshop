---
title: 'Módulo 2 - Respuesta de la Solicitud'
weight: 40
---

Cuando Step Functions llama a otro servicio usando estado `Tarea`, el patrón por defecto es [Respuesta de la Solicitud](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-default). Con este patrón de integración, Step Functions llamará al servicio y luego inmediatamente procederá con el siguiente estado. El estado `Tarea` no esperará a que la tarea lanzada termine.

En este modulo ejecutarás una `Tarea` usando el patrón Respuesta de la Solicitud.

**Duración estimada: 15 minutos**
