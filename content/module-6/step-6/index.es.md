---
title: 'Usar funciones intrínsecas para aumentar el procesamiento de datos'
weight: 86
---

El lenguaje de Amazon States (ASL) proporciona varias funciones intrínsecas, también conocidas como `intrinsics`, que le ayudan a realizar operaciones básicas de procesamiento de datos sin usar un estado de tarea.
Los ejemplos de operaciones básicas incluyen operaciones matemáticas, creación de ID's únicos o unión de objetos JSON. Puede usar `intrinsics` como `States.MathAdd`, `States.UUID` o `States.JsonMerge` en su flujo de trabajo para evitar sobrecargar una función Lambda al realizar esas operaciones.

Para una lista completa de `intrinsics`, vea la página de documentación [aquí](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-intrinsic-functions.html).

En esta sección, usará `States.MathAdd` para sumar dos números sin necesidad de usar una función Lambda para realizar la operación.
1. Vuelva a navegar a Workflow Studio para la máquina de estados `InputOutputProcessingMachine`.
2. Agregue un nuevo `Pass State` a la máquina de estados después del estado Lambda Invoke. Tenga en cuenta que no está limitado a ustilizar `Pass State` para `intrinsics`, podrá usarlos en cualquier estado que admita parámetros.

![Pass State Input](/static/img/module-6/pass-state-diagram.png)

3. En la pestaña `Input` del `Pass State`, complete el siguiente valor en el campo de texto del parámetro. Tenga en cuenta que deberá agregar el sufijo `.$` al usar intrínsecos.
    ```json
      {
        "Sum.$": "States.MathAdd($.value1, $.value2)"
      }
    ```

![Pass State Input](/static/img/module-6/pass-state-input-intrinsic.png)

4. A continuación salve las modificaciones, haga clic en **Start execution** y use el JSON a continuación como entrada.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "Un comentario de entrada.",
   "data": {
      "value1": 23,
      "value2": 17
   },
   "extra": "foo",
   "lambda": {
      "who": "AWS Step Functions"
   }
}
:::
5. Una vez que la ejecución sea exitosa, revise la salida en la pestaña `Execution input and output`. Verá que el campo sum tiene la suma de value1 y value2 de la entrada.

![Execution Output](/static/img/module-6/intrinsic-execution-output.png)

::alert[**Enhorabuena!** Usó una función intrínseca para realizar el procesamiento de datos básico sin necesidad de escribir código alguno!]{type="success"}

