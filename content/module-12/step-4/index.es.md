---
title: 'Registro de historial de ejecución con registros de Amazon CloudWatch'
weight: 144
---

Los flujos de trabajo estándar registran el historial de ejecución en AWS Step Functions, aunque también puede configurar el registro en Amazon CloudWatch Logs de manera opcional. Cuando crea un flujo de trabajo estándar, no se configura para habilitar el registro en CloudWatch Logs de manera predeterminante. Para configurar el registro, puede pasar el parámetro LoggingConfiguration al usar CreateStateMachine o UpdateStateMachine. CloudWatch Logs ofrece varias ventajas para el análisis de archivos de registro en comparación con el registro predeterminado, incluyendo la capacidad de analizar más a fondo sus datos mediante CloudWatch Logs Insights. Para obtener más información, consulte [Análisis de los datos de registros con Amazon CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html). Para comprender las políticas de IAM necesarias para registrarse en CloudWatch Logs, lea [Políticas de IAM para iniciar sesión en CloudWatch Logs](https://docs.aws.amazon.com/step-functions/latest/dg/cw-logs.html#cloudwatch-iam-policy).

## Configurar CloudWatch Logs

1. Abra la [Consola de Step Functions](https://console.aws.amazon.com/states/home) en su consola de AWS. Asegúrese de estar en la región correcta.

2. Haga clic en **State machines** en la navegación izquierda. Verá la máquina de estado llamada DetectSentimentStateMachine-XXXX desplegada para usted como parte de este laboratorio.

3. Haga clic en la máquina de estado **DetectSentimentStateMachine-XXXX**.

4. En la página DetectSentimentStateMachine, haga clic en la pestaña **Logging**. Verá que el `Log Level` está OFF, lo que indica que el registro de CloudWatch no está habilitado.

![CW Log disabled](/static/img/module-12/cw-log-disabled.png)

Habilite el registro de CloudWatch.

5. Haga clic en **Edit** en la parte superior de la página.

6. En la página `Edit DetectSentimentStateMachine`, desplácese hacia abajo para cambiar el nivel de registro bajo Registro a **ALL** y deje el resto como predeterminado.

![CW Log enabled](/static/img/module-12/cw-logging-enabled.png)

7. Haga clic en **Guardar** en la parte superior de la página.

8. En el cuadro de diálogo de rol de IAM, haga clic en **Guardar de todos modos**.

Vuelva a la página DetectSentimentStateMachine y espere unos minutos. Actualice la página y verá la sección CloudWatch Logs Insights poblada con registros.

   ![CW Logs](/static/img/module-12/cw-logs.png)

## Consultar CloudWatch Logs Insights

1. Abra la [consola de CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Haga clic en **Logs Insights** debajo de Logs en el menú de navegación izquierdo.

2. En la página Logs Insights, seleccione el grupo de registros **/aws/vendedlogs/states/DetectSentimentStateMachine-XXX-Logs**.

   ![CWL Vended](/static/img/module-12/cwl-vendedlogs.png)

3. En el campo de texto, copie y pegue la siguiente consulta y haga clic en **Ejecutar consulta**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, type
| stats count(*) as typeCount by type 
| sort typeCount desc
:::

Esta consulta de CloudWatch Log Insights muestra las estadísticas de varios tipos de ejecución.

   ![CWL query](/static/img/module-12/cwl-query.png)

   Desplácese hacia abajo en la sección de resultados para revisar los resultados completos. Verá los resultados TaskFailed y ExecutionFailed.

   ![CWL failed](/static/img/module-12/cwl-failed.png)

12. Para identificar la causa de las ejecuciones fallidas, copie y pegue la siguiente consulta en el campo de texto de CloudWatch Log Insights y haga clic en **Ejecutar consulta**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, execution_arn, details.error, details.cause
| filter type = 'TaskFailed'
| limit 100
:::

![CWL failureReasons 1](/static/img/module-12/cwl-failureReasons-1.png)

![CWL CWL failureReasons 2](/static/img/module-12/cwl-failureReasons-2.png)

Estos errores indican que las fallas en la ejecución de las funciones de paso se debieron al rendimiento limitado de DynamoDB. En el próximo módulo, utilizará X-Ray para investigar con más detalle estos fallos.
