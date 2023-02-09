---
title: 'Módulo 12 - Observabilidad'
weight: 140
---
La observabilidad te ayuda a entender lo que está sucediendo en tus sistemas y aplicaciones. Ganar observabilidad te ayuda a detectar, investigar y remediar problemas.

Los tres pilares de la observabilidad son:
  - Métricas
  - Registros
  - Trazas

Las *Métricas* son una representación numérica de los datos medidos en intervalos de tiempo. Las métricas proporcionan datos sobre el rendimiento de tus sistemas. Puedes pensar en una métrica como una variable individual utilizada para monitorear un aspecto de su sistema. Cuando combinas todas estas métricas individuales, puedes ver cómo se está ejecutando tu aplicación a lo largo del tiempo.

Los *Registros* ayudan a mantener un registro de los eventos que han ocurrido dentro de tu aplicación o sistema. Los registros se generan con fecha y hora, y pueden incluir eventos como fallas, errores, transformaciones de estado o incluso quién accedió a tu sistema en un momento dado. Los registros se pueden grabar en formatos no estructurados, semiestructurados o estructurados.

Las *Trazas* son representaciones de una serie de eventos distribuidos causalmente relacionados. Las trazas pueden codificar los flujos de solicitud de extremo a extremo a través de un sistema distribuido.

Monitorear las métricas, los registros y las trazas puede ayudarte a entender la disponibilidad, el rendimiento y la salud de tus aplicaciones. AWS proporciona varias herramientas que puedes usar con Step Functions para monitorear estos tres pilares de observabilidad.

Revisar la documentación:
- [Registros y monitoreo en AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/monitoring-logging.html)
- [EventBridge para cambios en el estado de ejecución de Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/cw-events.html)
- [AWS X-Ray y Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html)

**Duración estimada: 30 minutos**
