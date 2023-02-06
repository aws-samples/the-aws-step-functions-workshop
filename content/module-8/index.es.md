---
title: 'Módulo 8 - Manejo de errores'
weight: 100
---
Pueden saltar errores en cualquier estado durante la ejecución. Los errores pueden ocurrir por varias razones:

- Problemas en la definición de la máquina de estado (por ejemplo, no hay regla coincidente en un estado `Choice`)

- Fallos de tareas (por ejemplo, una excepción en una función Lambda)

- Problemas transitorios (por ejemplo, eventos de partición de red)

De manera predeterminada, cuando un estado informa un error, Step Functions hace que la ejecución fallé completamente. Sin embargo, Step Functions tiene características de manejo de errores que le permiten volver a intentar o capturar estados que fallan. Las características de manejo de errores pueden definir protocolos de reintento y también capturar y manejar una variedad de condiciones de error.

Este módulo demuestra **error handling** mediante el uso de funciones Lambda para simular errores que se manejan utilizando los campos `Retry` y `Catch`.

Revisa la documentación:
- [Error handling in Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html)
- [Error handling in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html)

**Duración estimada: 20 minutos**
