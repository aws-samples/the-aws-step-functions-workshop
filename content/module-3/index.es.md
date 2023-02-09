---
title: 'Módulo 3 - Ejecutar un trabajo (.sync)'
weight: 50
---

Para servicios integrados como AWS Batch y Amazon ECS, Step Functions puede esperar a que una tarea se complete antes de avanzar al siguiente estado. Este patrón de orquestación de tareas se llama [Ejecutar un trabajo (.sync)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-sync) en la documentación. Para ver una lista de los servicios integrados que admiten sincronización, vea [Integraciones optimizadas para Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).

Para ver un ejemplo de un proyecto de computación de alto rendimiento (HPC) que utiliza AWS Batch, Step Functions y Ejecutar un trabajo (.sync), vea [este blog post](https://aws.amazon.com/blogs/compute/orchestrating-high-performance-computing-with-aws-step-functions-and-aws-batch/).

En este módulo configurará y ejecutará una tarea sincronizada utilizando **Ejecutar un trabajo (.sync)**.

**Duración estimada: 10 minutos**
