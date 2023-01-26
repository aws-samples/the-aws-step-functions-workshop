---
title: 'Módulo 7 - API Gateway, estado parallel, flujos de trabajo Express'
weight: 90
---
Amazon API Gateway es un servicio completamente administrado que facilita a los desarrolladores crear, publicar, mantener, monitorear y asegurar API. Step Functions se integra directamente con API Gateway, lo que le permite activar la ejecución de una máquina de estados con una solicitud HTTP. API Gateway se puede usar tanto con flujos de trabajo Standard como Express. Las integraciones pueden ser síncronas o asíncronas.

El estado `Parallel` puede permitir un procesamiento de datos más rápido al crear un número fijo de ramas paralelas de ejecución en su máquina de estados.

En este módulo aprenderá sobre cómo API Gateway se integra con los flujos de trabajo Express a través de patrones asíncronos y síncronos. También aprenderá cómo usar el estado `parallel` para crear múltiples ramas concurrentes de lógica.

![API Gateway to Step Functions architecture](/static/img/module-7/architecture.png)

Aprenda más sobre [Estados paralelos](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-parallel-state.html).

Aprenda más sobre [Integración de API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-integration-types.html).

**Duración estimada: 25 minutos**
