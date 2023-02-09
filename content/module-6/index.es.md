---
title: 'Módulo 6: Procesamiento de entrada y salida'
weight: 80
---
Una ejecución de Step Functions recibe texto JSON como entrada y pasa esa entrada al primer estado del flujo de trabajo. Cada estado individual recibe un JSON como entrada y, por lo general, pasa un JSON como salida al siguiente estado. Comprender cómo fluye esta información de un estado a otro y aprender a filtrar y manipular estos datos es fundamental para diseñar e implementar flujos de trabajo de forma efectiva en Step Functions.

En Amazon State Language (ASL), estos campos filtran y controlan el flujo de un JSON de un estado a otro:

- `InputPath`
- `OutputPath`
- `ResultPath`
- `Parameters`
- `ResultSelector`

Lea la documentación para obtener más información sobre [Procesamiento de entrada y salida](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-input-output-filtering.html).

**Duración estimada: 25 minutos**