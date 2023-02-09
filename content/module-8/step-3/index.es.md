---
title: 'Manejar un fallo utilizando Reintento'
weight: 103
---

Los estados `Task` y `Parallel` pueden tener un campo llamado `Retry`, cuyo valor debe ser un arreglo de objetos conocidos como reintentadores. Un reintentador individual representa un cierto número de reintentos, generalmente en intervalos de tiempo crecientes.

En el ejercicio a continuación, crearás una definición ASL que invoca una función Lambda. La función Lambda está diseñada para fallar. Implementarás un `Retry` para esta función, estableciendo un número máximo de intentos con una tasa de retroceso exponencial entre los reintentos.

1. Localiza la función **ErrorHandlingCustomErrorFunction** [Lambda function](https://console.aws.amazon.com/lambda/home). Copia la función ARN y revisa el código. Observa que el código está configurado para lanzar un error.

![Lambda function throws FooError](/static/img/module-8/error-handling-lambda-foo-error.png)

2. Ahora localiza la [maquinaria de estado](https://console.aws.amazon.com/states/home) que comienza por **ErrorHandlingStateMachineWithRetry-...** . Haz clic en su enlace y haz clic en el botón **Edit** en la esquina superior derecha de la pantalla.

3. En el campo `Resource`, reemplaza el valor actual con el ARN de la función Lambda copiada en el paso 1. Cuando la máquina de estado invoca esta función, la función fallará. Para ver el fallo, haz clic en **Save** y luego en **Start execution**. Acepte la entrada predeterminada y haz clic en **Start execution** de nuevo.

![Replace Lambda function ARN](/static/img/module-8/error-handling-state-machine-retry.png)

4. Ahora implemente un `Retry`. Copia el siguiente código y pega en la línea 8 entre el nodo `Resource` y el nodo `End`.

```bash
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
```

5. Revisa los parámetros de manejo de errores. Estos parámetros definen el comportamiento del `Retry`.

- ErrorEquals (Requerido)

  > Un arreglo no vacío de cadenas que coinciden con los nombres de errores. Cuando un estado informa un error, Step Functions escanea los reintentadores. Cuando el nombre de error aparece en este arreglo, se implementa la política de reintento descrita en este reintentador.

- IntervalSeconds (Opcional)

  > Un entero que representa el número de segundos antes del primer intento de reintento (1 de forma predeterminada). IntervalSeconds tiene un valor máximo de 99999999.

- MaxAttempts (Opcional)

  > Un entero positivo que representa el número máximo de intentos de reintento (3 de forma predeterminada). Si el error vuelve a ocurrir más veces de lo especificado, los reintentos cesan y el manejo de errores normal continúa. Un valor de 0 especifica que el error o errores nunca se reintentan. MaxAttempts tiene un valor máximo de 99999999.

- BackoffRate (Opcional)

  > El multiplicador por el cual se aumenta el intervalo de reintento durante cada intento (2.0 de forma predeterminada).

Revisa la documentación para obtener más información sobre [parámetros de manejo de errores](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html).

6. Haz clic en **Save** y luego en **Start execution**. Acepte la entrada predeterminada y haz clic en **Start execution** de nuevo.

7. Para ver su mensaje de error personalizado, selecciona `StartExecution` en el panel inspector de gráficos y revisa la pestaña **Input and output**.
   ![Failure using Retry output](/static/img/module-8/error-handling-custom-error-retry-output.png)

8. Desplázate hacia abajo y revisa la tabla **Events** para obtener más detalles sobre la ejecución. Observa los reintentos en el historial de eventos.
   ![Failure using Retry event history](/static/img/module-8/error-handling-custom-error-retry-event-history.png)

### ¿Tienes problemas?

Su definición ASL debe ser similar al fragmento de abajo. Recuerde reemplazar el ARN de la función Lambda en el nodo `Resource`.

```bash
{
  "Comment": "A state machine calling an AWS Lambda function with Retry",
  "StartAt": "StartExecution",
  "States": {
    "StartExecution": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:FailFunction",
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "End": true
    }
  }
}
```

Cuando estés listo puedes ir a la siguiente página.
