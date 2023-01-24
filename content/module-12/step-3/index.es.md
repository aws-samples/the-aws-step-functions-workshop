---
title: 'Monitorear ejecuciones con Amazon CloudWatch Metrics'
weight: 143
---

Monitorear métricas es importante para mantener la confiabilidad, disponibilidad y rendimiento de tus flujos de trabajo.

En este taller se desplegará una máquina de estado llamada *DetectSentimentStateMachine* y algunos otros recursos.

![Máquina de estado DetectSentiment](/static/img/module-12/state-machine.png)

Esta máquina de estado acepta una cadena de entrada, detecta el sentimiento del texto en la cadena y registra el resultado del análisis en una tabla de Amazon DynamoDB. El flujo de trabajo invoca una función Lambda que llama a Amazon Comprehend para realizar el análisis de sentimientos. Esta máquina de estado se activa una vez por minuto con una regla de Amazon EventBridge.

En este ejercicio, utilizarás CloudWatch Metrics para monitorear las ejecuciones del flujo de trabajo *DetectSentimentStateMachine*.

Las siguientes métricas de ejecución de Step Functions están disponibles en CloudWatch:
- ExecutionTime
- ExecutionThrottled
- ExecutionsAborted
- ExecutionsFailed
- ExecutionsStarted
- ExecutionsSucceeded
- ExecutionsTimedOut

Más detalles sobre estas métricas se pueden encontrar [aquí](https://docs.aws.amazon.com/step-functions/latest/dg/procedure-cw-metrics.html#cloudwatch-step-functions-execution-metrics).

1. Navega a la [consola de CloudWatch](https://console.aws.amazon.com/cloudwatch/home) en su consola de AWS. Asegúrate de estar en la región correcta.

2. Bajo `Métricas` en el menú de navegación izquierdo, Haz clic en **Todas las métricas**. Encuentra el cuadro de métricas llamado **Estados** y Haz clic en él.

![CW All Metrics States](/static/img/module-12/cw-all-metrics-states.png)

3. Haz clic en **Métricas de ejecución**.

![Execution Metrics](/static/img/module-12/cw-states-execution-metrics.png)

4. Selecciona todas las métricas listadas para `DetectSentimentStateMachine`.

![DetectSentiment Metrics](/static/img/module-12/cw-detect-sentiment-metrics.png)

5. Haz clic en la pestaña **Métricas diagramadas**. Actualiza la columna `Estadística` de `ExecutionTime` a **Media** y la columna `Estadística` para el resto de las métricas a **Suma**. En la parte superior derecha, cambie la leyenda de **Línea** a **Número**.

   ![Suma y promedio](/static/img/module-12/cw-metrics-sum-avg.png)

6. Haz clic en el lápiz de edición junto al título del gráfico, escriba **Métricas de ejecución** y Haz clic en **Aplicar**.

7. En la parte superior derecha, Haz clic en el menú desplegable **Acciones** y elige **Añadir al panel**.

-  En la página Añadir al panel, Haz clic en **Crear nuevo**.
- Escriba *DetectSentiment* para el nombre del panel y Haz clic en **Crear**.
- Para **tipo de widget**, selecciona Número.
- Haz clic en **Añadir al panel**.

   ![Métricas CW](/static/img/module-12/cw-add-dashboard.png)

8. Elige **Guardar panel**.

Ahora puedes ver las métricas de ejecución para DetectSentiment State Machine Step Functions. Notará que hay ejecuciones que han fallado, indicadas por las métricas ExecutionsFailed.

   ![Métricas del panel](/static/img/module-12/cw-dashboard.png)

En los siguientes módulos, utilizará CloudWatch Logs y trazas de X-Ray para depurar e identificar la causa raíz de estos fallos.