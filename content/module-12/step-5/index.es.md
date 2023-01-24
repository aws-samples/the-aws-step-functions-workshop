---
title: 'Depurar ejecuciones fallidas con AWS X-Ray Traces'
weight: 145
---

Puedes usar AWS X-Ray para visualizar las integraciones en tu máquina de estados, para identificar cuellos de botella de rendimiento y para resolver problemas de solicitudes fallidas. Cuando tu máquina de estados envía datos de trazas a X-Ray, X-Ray procesa los datos para generar un mapa de servicios y resúmenes de trazas buscables.

Con X-Ray habilitado para tu máquina de estados, puedes trazar los caminos de tus solicitudes, lo que te brinda una visión detallada visual de tu flujo de trabajo completo. Puedes usar los mapas de servicios de X-Ray para ver la latencia de las solicitudes, incluidos cualquier servicio de AWS que esté integrado con X-Ray. También puedes configurar y personalizar las reglas de muestreo en X-Ray para controlar la frecuencia de las solicitudes registradas.

Para obtener más información, lea [AWS X-Ray y Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html).

## Habilitar la traza X-Ray en DetectSentimentStateMachine.

1. Navega a [Consola de Step Functions](https://console.aws.amazon.com/states/home). Asegúrate de estar en la región correcta.

2. Haz clic en **DetectSentimentStateMachine** Máquina de estado.

3. En la página `DetectSentimentStateMachine`, haz clic en **Edit**.

4. En la sección `Tracing` de la página de edición, selecciona **Enable X-Ray tracing**.

:::alert{header="Importante" type="warning"}
Para trazar ejecuciones con X-Ray, el rol de ejecución de Step Functions debe tener permisos de X-Ray. Puedes dejar que Step Functions cree un nuevo rol para ti con los permisos necesarios seleccionando "Crear nuevo rol" en Permisos, o agregarlos manualmente a tu rol existente. Esto ya lo has hecho anteriormente.
:::

5. Haz clic en **Guardar** en la parte superior de la página.

6. Navega a [X-Ray](https://console.aws.amazon.com/xray/home) en la consola de AWS.

Espera unos minutos hasta que la consola de X-Ray se cargue con el Mapa de servicios. Refresca la página, si es necesario. Verás el siguiente Mapa de servicios para DetectSentimentStateMachine. 

   ![Service Map](/static/img/module-12/x-ray-service-map.png)

Este mapa de servicios muestra que su máquina de estado interactúa con AWS Lambda y Amazon DynamoDB. La leyenda roja en la máquina de estado DetectSentiment indica fallos. La leyenda morada en el nodo sentiment-table indica limitaciones de velocidad.

7. Haz clic en el nodo **sentiment-table** para investigar estas limitaciones de velocidad.

8. En el panel de detalles del servicio en la derecha, selecciona **Limitaciones** y Haz clic en **Ver rastreos**

   ![View Traces](/static/img/module-12/x-ray-view-traces.png)

9. En la página `Trazas` bajo la lista de trazas, Haz clic en una de las trazas. 

   ![View Traces](/static/img/module-12/x-ray-traces-list.png)

10. En la página de detalles de la traza, verás un icono de error en el segmento AWS::StepFunctions::StateMachine.

    ![View Traces](/static/img/module-12/x-ray-trace-error.png)

11. Más abajo en la traza, hay un error junto al subsegmento Record Transaction. Haz clic en el icono de error.

    ![View Traces](/static/img/module-12/x-ray-exception.png)

El error se debe a una limitación en la capacidad provisionada de la tabla de DynamoDB. El rendimiento solicitado excedió el nivel de capacidad provisionada configurado. Para resolver el problema, puedes reducir el rendimiento solicitado disminuyendo la frecuencia de sus escrituras o puedes aumentar su capacidad aumentando las unidades de escritura provisionadas o cambiando el modo de facturación de DynamoDB de provisionado a bajo demanda.