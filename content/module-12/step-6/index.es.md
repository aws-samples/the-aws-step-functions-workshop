---
title: 'Arreglar los errores y verificar las trazas de X-Ray'
weight: 146
---

## Actualizar las unidades de capacidad provisionadas de DynamoDB

1. Navega hasta la [consola de DynamoDB](https://console.aws.amazon.com/dynamodbv2/home). Asegúrese de estar en la región correcta.

2. Haz clic en **Tablas** en el menú izquierdo.

3. Haz clic en la **sentiment-table** en el panel central.

4. En la pestaña de configuración adicional, Haz clic en **Editar**.

5. En la página de edición de capacidad de lectura y escritura, actualiza las unidades de capacidad provisionadas bajo **Unidades escritura aprovisionadas** a **10**

![Update DDB](/static/img/module-12/ddb-wcu.png)

:::alert{header="Importante" type="warning"}
Cambiar las unidades de capacidad provisionadas en una tabla de Amazon DynamoDB puede generar costos adicionales. Por favor revisa el [precio de Amazon DynamoDB](https://aws.amazon.com/dynamodb/pricing/) para la capacidad provisionada. Proporcionaremos instrucciones para eliminar estos recursos al final de este módulo.
:::

6. Haz clic en **Guardar cambios**.

Espera unos minutos hasta que la nueva configuración de capacidad se haya actualizado correctamente.
   
   ![Update DDB](/static/img/module-12/ddb-updated.png)

## Verificar la solución con X-Ray

1. Navega hasta la [consola de X-Ray](https://console.aws.amazon.com/xray/home) para buscar los cuellos de botella.

2. Actualiza el intervalo de tiempo a 1 min.

   ![No throttles](/static/img/module-12/x-ray-update-time.png)

Deberías ver ahora que no hay más fallos o cuellos de botella. 

   ![No throttles](/static/img/module-12/x-ray-no-throttles.png)

Si revisa las métricas de CloudWatch para las ejecuciones de Step Functions, también deberías ver que ExecutionsFailed ha bajado a 0. 

   ![Zero Failed executions](/static/img/module-12/cw-states-execution-metrics-0.png)

   ::alert[¡Enhorabuena! Has completado con éxito el módulo de observabilidad.]{type="success"}
