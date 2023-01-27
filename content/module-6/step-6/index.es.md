---
title: 'Usar funciones intrínsecas para aumentar el procesamiento de datos'
weight: 86
---

El lenguaje de Amazon States (ASL) proporciona varias funciones intrínsecas, también conocidas como `intrinsics`, que te ayudan a realizar operaciones básicas de procesamiento de datos sin usar un estado de tarea.
Los ejemplos de operaciones básicas incluyen operaciones matemáticas, creación de ID's únicos o unión de objetos JSON. Puedes usar `intrinsics` como `States.MathAdd`, `States.UUID` o `States.JsonMerge` en tu flujo de trabajo para evitar sobrecargar una función Lambda al realizar esas operaciones.

Para una lista completa de `intrinsics`, ve a la página de documentación [aquí](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-intrinsic-functions.html).

En esta sección, usarás `States.MathAdd` para sumar dos números sin necesidad de usar una función Lambda para realizar la operación.
1. Vuelve a navegar a Workflow Studio para la máquina de estados `InputOutputProcessingMachine`.
2. Agrega un nuevo `Pass State` a la máquina de estados después del estado Lambda Invoke. Ten en cuenta que no está limitado a utilizar `Pass State` para `intrinsics`, podrás usarlos en cualquier estado que admita parámetros.

![Pass State Input](/static/img/module-6/pass-state-diagram.png)

3. En la pestaña `Input` del `Pass State`, completa el siguiente valor en el campo de texto del parámetro. Ten en cuenta que deberás agregar el sufijo `.$` al usar intrínsecos.
    ```json
      {
        "Sum.$": "States.MathAdd($.value1, $.value2)"
      }
    ```

![Pass State Input](/static/img/module-6/pass-state-input-intrinsic.png)

4. A continuación salva las modificaciones, haz clic en **Start execution** y use el JSON a continuación como entrada.
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
5. Una vez que la ejecución sea exitosa, revisa la salida en la pestaña `Execution input and output`. Verás que el campo `sum` tienes la suma de value1 y value2 de la entrada.

![Execution Output](/static/img/module-6/intrinsic-execution-output.png)

::alert[**Enhorabuena!** Usaste una función intrínseca para realizar el procesamiento de datos básico sin necesidad de escribir código alguno!]{type="success"}
