---
title: 'Monitorización de flujos de trabajo Express'
weight: 97
---

La monitorización de flujos de trabajo Express requiere el uso de herramientas diferentes a las que usas para los flujos de trabajo estándar. En lugar de utilizar el inspector de gráficos y los widgets de historial de eventos de ejecución como lo harías con los flujos de trabajo estándar, con flujos de trabajo Express como `ParallelProcessingMachine` utilizarías Amazon CloudWatch para la monitorización.

1. Navega a la consola de Step Functions y selecciona el `ParallelProcessingMachine`.
2. Todo el historial de ejecución se envía a los registros de Amazon CloudWatch. Utiliza las pestañas de `Monitoring` y `Logging` en la consola de Step Functions para obtener visibilidad en las ejecuciones de los flujos de trabajo Express.
3. La pestaña de `Monitoring` muestra seis gráficos con métricas de Amazon CloudWatch para errores de ejecución, ejecuciones correctas, duración de ejecución, duración facturada, memoria facturada y ejecuciones iniciadas.
    ![](/static/img/module-7/express-workflows-metrics.png)
4. Navega a la pestaña de `Logging` para ver los registros recientes y la configuración de registros, con un enlace a los registros de Amazon CloudWatch.
    ![](/static/img/module-7/express-workflows-logs.png)
5. Haz clic para ver el grupo de registros de Amazon CloudWatch y ver el historial detallado allí.

::alert[**¡Enhorabuena!** Acabas de monitorizar las ejecuciones para tu flujo de trabajo Express de Step Functions.]{type="success"}
