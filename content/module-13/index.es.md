---
title: 'Módulo 13 - Flujos de trabajo anidados de Express'
weight: 150
---
A medida que adquieres más experiencia con Step Functions y aumenta la complejidad de tus máquinas de estado, es posible que comiences a buscar formas de simplificar y optimizar las ejecuciones de tus máquinas de estado. Anidar flujos de trabajo dentro de otros flujos de trabajo es una herramienta poderosa. Desde una perspectiva de modularidad, los flujos de trabajo anidados te permiten crear máquinas de estado reutilizables que pueden ser ejecutadas por otros flujos de trabajo, promoviendo la reutilización. Anidar flujos de trabajo de diferentes tipos, como un flujo de trabajo Express anidado dentro de un flujo de trabajo Estándar, puede ayudarte a reducir el costo. Para los flujos de trabajo Estándar, pagas por transición de estado, y los flujos de trabajo grandes y complejos pueden volverse costosos a gran escala. Una forma de reducir el costo es determinar si algunos pasos podrían moverse a un flujo de trabajo Express. A diferencia de los flujos de trabajo Estándar, los flujos de trabajo Express son cobrados por el tiempo que se ejecutan, independientemente del número de transiciones de estado, así como por el número de ejecuciones.

Los flujos de trabajo Express difieren de los flujos de trabajo Estándar en varios sentidos:

1. Los flujos de trabajo Estándar tienen un modelo de ejecución de "exactamente una vez", mientras que los flujos de trabajo Express son "al menos una vez".
1. Los flujos de trabajo Express no admiten ciertos métodos de invocación, como `sync` y `waitForTaskToken`.
1. Los flujos de trabajo Express tienen una duración máxima de 5 minutos, mientras que los flujos de trabajo Estándar pueden ejecutarse durante hasta 365 días.

Para una comparación completa de los flujos de trabajo Estándar y Express, consulta la [documentación](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html).

A medida que examina sus flujos de trabajo, es posible que identifique pasos que se podrían mover a un flujo de trabajo de Express, quizás porque son [idempotentes](https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-idempotent/), lo que significa que se pueden ejecutar más de una vez sin afectar el resultado final. En ese caso, podría crear un flujo de trabajo de Express que contenga esos pasos y luego ejecutar ese flujo de trabajo anidado desde el flujo de trabajo Estándar existente, logrando ahorros de costos al hacerlo.

Este módulo lo guiará a través del proceso utilizando la consola de AWS, pero también puede desarrollar flujos de trabajo anidados escritos en [Amazon States Language (ASL)](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) y desplegados utilizando [AWS CloudFormation](https://aws.amazon.com/cloudformation/) o [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/), utilizando [AWS Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_stepfunctions_tasks.StepFunctionsStartExecution.html), o utilizando herramientas de infraestructura como código de terceros como Terraform y Serverless Framework.

Revise la documentación:

- [Flujos de trabajo Estándar vs. Express](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Optimización de costos utilizando flujos de trabajo Express](https://docs.aws.amazon.com/step-functions/latest/dg/cost-opt-exp-workflows.html)
- [Building cost-effective AWS Step Functions workflows](https://aws.amazon.com/blogs/compute/building-cost-effective-aws-step-functions-workflows/)
- [Ejemplo de puntos de control selectivos](https://docs.aws.amazon.com/step-functions/latest/dg/sample-project-express-selective-checkpointing.html)

**Duración estimada: 20 minutos**
