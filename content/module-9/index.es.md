---
title: 'Módulo 9 - Integraciones de servicio AWS SDK'
weight: 110
---

AWS Step Functions se integra con muchos otros servicios de AWS. Puedes utilizar las [integraciones de servicio con AWS SDK de Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/supported-services-awssdk.html) para llamar directamente a más de 220 servicios de AWS desde su máquina de estados, lo que le da acceso a más de 10,000 acciones de API.

Para usar las integraciones de AWS SDK, especifique el nombre del servicio y la llamada de la API. Algunas integraciones requieren parámetros y puedes especificar opcionalmente un patrón de integración de servicio. Ten en cuenta que la acción de la API será en Camel case (camelCase), y los nombres de los parámetros serán en Pascal case (PascalCase). Puedes usar el lenguaje de estados de Amazon para especificar una acción de la API de AWS en el campo Recurso de un estado de tarea. Para hacer esto, usa la siguiente sintaxis:

`arn:aws:states:::aws-sdk:serviceName:apiAction.[serviceIntegrationPattern]`

**Ejemplos**

- Para describir instancias de Amazon EC2, utiliza la sintaxis: `arn:aws:states:::aws-sdk:ec2:describeInstances`. Esto devolverá como salida el valor de retorno de la llamada de la API de Amazon EC2 describeInstances.

- Para listar los buckets en Amazon S3, utiliza `arn:aws:states:::aws-sdk:s3:listBuckets`. Esto devolverá como salida el valor de retorno de la llamada de la API de Amazon S3 listBuckets.

- Para iniciar una ejecución anidada en Step Functions utiliza la sintaxis: `arn:aws:states:::aws-sdk:sfn:startExecution`. Luego, agrega StateMachineArn como parámetro. Esto devolverá como salida el valor de retorno del flujo de trabajo anidado de Step Functions.

**Duración estimada: 10 minutos**

