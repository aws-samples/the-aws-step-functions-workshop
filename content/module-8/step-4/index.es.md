---
title: 'Manejar un fallo utilizando Catch'
weight: 104
---

Los estados `Task`, `Map` y `Parallel` pueden contener un campo llamado `Catch`. El valor de este campo debe ser una matriz de objetos, conocidos como atrapadores. Cada atrapador se puede configurar para atrapar un tipo específico de error. ASL define un conjunto de cadenas incorporadas que nombran errores conocidos, todos comenzando con el prefijo `States.`. Los atrapadores también pueden atrapar errores personalizados. Cada atrapador se puede configurar para reenviar a un estado de **fallback** específico. Cada estado de fallback puede implementar lógica de manejo de errores. Los tipos de error incorporados incluyen:

- `States.ALL` - un comodín que coincide con cualquier nombre de error conocido
- `States.DataLimitExceeded` - una salida excede el cupo
- `States.Runtime` - una excepción de tiempo de ejecución no se pudo procesar
- `States.HeartbeatTimeout` - un estado Task no pudo enviar un latido
- `States.Timeout` - un estado Task se agotó el tiempo
- `States.TaskFailed` - un estado Task falló durante la ejecución
- `States.Permissions` - un estado Task tuvo privilegios insuficientes

Cuando un estado tiene tanto campos `Retry` como `Catch`, Step Functions utiliza el reintentador primero, y solo después aplica la transición de atrapador correspondiente si la política de reintento no logra resolver el error.

Lea la documentación para obtener más información sobre [Error names](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html).

En este ejercicio, configurará una máquina de estado que atrapará un error personalizado y un error `States.Timeout` utilizando el campo `Catch`.

### Atrapar un error personalizado

1. Ubique la función **ErrorHandlingCustomErrorFunction** [Lambda function](https://console.aws.amazon.com/lambda/home). Copia el ARN de la función y revisa el código. Observa que el código lanza un error llamado `CustomError`.

![Lambda function throws CustomError](/static/img/module-8/error-handling-lambda-function-custom-error.png)

2. Ahora ubique la máquina de estado **ErrorHandlingStateMachineWithCatch-...** [state machine](https://console.aws.amazon.com/states/home). Haz clic en su enlace y haz clic en el botón **Edit** en la esquina superior derecha de la pantalla.
3. En el campo `Resource`, reemplaza el valor actual con el ARN de la función Lambda copiada en el paso 1. Cuando la máquina de estado invoca esta función, la función fallará con el `CustomError`.

![Replace Lambda function ARN](/static/img/module-8/error-handling-state-machine-catch.png)

4. Revisa el bloque `Catch` de su definición ASL. Observa que contiene tres atrapadores. El primer atrapador está configurado para atrapar un error llamado `CustomError`. Cuando atrapa este error, pasa el control de flujo al estado de fallback `CustomErrorFallback`.

![Catch CustomError](/static/img/module-8/error-handling-state-machine-catch-custom-error.png)

5. Haz clic en **Save** y luego en **Start execution**. Acepte la entrada predeterminada y haz clic en **Start execution** nuevamente.

6. Ve a la pestaña **Execution input and output** para ver la salida de su flujo de trabajo. Debería mostrar `This is a fallback from a custom Lambda function exception`

7. Para ver la salida del estado de fallback, selecciona el estado `CustomErrorFallback` en el inspector de gráficos y haz clic en la pestaña **Input and output**.

![Failure using Catch output](/static/img/module-8/error-handling-custom-error-catch-output.png)

8. Desplázate hacia abajo hasta la tabla **Events** para obtener más detalles.

![Failure using Catch event history](/static/img/module-8/error-handling-custom-error-catch-event-history.png)

### Atrapar un error de tiempo de espera

1. Ubique la función **ErrorHandlingSleep10Function** [Lambda function](https://console.aws.amazon.com/lambda/home). Copia el ARN de la función y revisa el código. Observa que la función está configurada para dormir durante 10 segundos.

   ![La función Lambda duerme durante 10 segundos](/static/img/module-8/error-handling-lambda-sleep10.png)

2. Ahora ubique la máquina de estados **ErrorHandlingStateMachineWithCatch-...** [state machine](https://console.aws.amazon.com/states/home). Haz clic en su enlace y haz clic en el botón **Editar** en la esquina superior derecha de la pantalla.

3. En el campo `Resource`, reemplaza el valor actual con el ARN de la función Lambda copiada en el paso 1. Cuando la máquina de estados invoca esta función, la función dormirá durante 10 segundos.

   ![Replace Lambda function ARN](/static/img/module-8/error-handling-state-machine-catch.png)

4. Observa el campo `TimeoutSeconds` para la tarea está configurado en 5 segundos. Observa el atrapador configurado para atrapar el error `States.Timeout`. Este atrapador envía al estado `TimeoutFallback`.

   ![Review the Timeout Catcher](/static/img/module-8/error-handling-state-machine-timeout.png)

5. Haz clic en **Save** y luego en **Start execution**. Acepte la entrada predeterminada y haz clic en **Start execution** de nuevo.

6. Ve a la pestaña **Execution input and output** para ver la salida de su flujo de trabajo. Debería mostrar `This is a fallback from a timeout Lambda function exception`

7. Para ver la salida del estado de fallback, selecciona el estado `TimeoutFallback` en el panel inspector de gráficos y haz clic en la pestaña **Input and output**.
   ![Failure using Catch output](/static/img/module-8/error-handling-timeout-error-catch-output.png)

8. Desplázate hacia abajo hasta la tabla **Events** para obtener más detalles
   ![Failure using Catch event history](/static/img/module-8/error-handling-timeout-error-catch-event-history.png)

   ::alert[¡Enhorabuena! Has completado con éxito el módulo de Manejo de errores.]{type="success"}