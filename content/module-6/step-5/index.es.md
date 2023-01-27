---
title: 'Use el simulador de flujo de datos para probar el procesamiento de datos'
weight: 85
---

1. Haz clic en el botón **Data Flow Simulator** en el Inspector de gráficos.

El simulador de flujo de datos permite a los desarrolladores simular el orden de procesamiento de datos que ocurre en un solo estado de tarea durante la ejecución. Esto ayuda a los desarrolladores a comprender cómo filtrar y manipular los datos a medida que fluyen de un estado a otro. Los desarrolladores pueden especificar una entrada JSON de inicio y evaluarla a través de cada una de las etapas del camino de procesamiento.

El simulador comienza en la etapa de `State Input`. El campo de entrada valida automáticamente el objeto JSON e resalta cualquier error de sintaxis.

![Data flow simulator](/static/img/module-6/simulator.png)

2. Utiliza el simulador de flujo de datos para simultar el procesamiento de los datos de entrada de `InputOutputProcessingMachine`. Reemplaza el `Input State` predeterminado con el JSON de a continuación y elige la etapa InputPath. Establezca InputPath en $.lambda.

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

![Data flow simulator](/static/img/module-6/input-path.png)

El panel izquierdo muestra el valor de entrada antes de que se aplique InputPath. El panel de la derecha muestra el valor de entrada después de que se aplique InputPath.

Los desarrolladores pueden utilizar el simulador de flujo de datos para implementar rápidamente el procesamiento de datos que necesitan en sus máquinas de estados.
Siéntete libre de seguir probando valores para los parámetros, ResultSelector y OutputPath dentro del simulador de flujo de datos. Tenga en cuenta que deberá reemplazar los valores predeterminados en todo el simulador de acuerdo a las transformaciones que quiera aplicar.

Para obtener más información sobre el simulador de flujo de datos, consulte el [AWS Blog](https://aws.amazon.com/blogs/compute/modeling-workflow-input-output-path-processing-with-data-flow-simulator/).

::alert[**¡Enhorabuena!** Usó el simulador de flujo de datos para practicar el procesamiento de entrada y salida con Amazon State Language!]{type="success"}


# Usar funciones intrínsecas para aumentar el procesamiento de datos

El lenguaje de Amazon States (ASL) proporciona varias funciones intrínsecas, también conocidas como `intrinsics`, que le ayudan a realizar operaciones básicas de procesamiento de datos sin usar un estado de tarea.
Los ejemplos de operaciones básicas incluyen operaciones matemáticas, creación de ID's únicos o unión de objetos JSON. Puedes usar `intrinsics` como `States.MathAdd`, `States.UUID` o `States.JsonMerge` en su flujo de trabajo para evitar sobrecargar una función Lambda al realizar esas operaciones.

Para una lista completa de `intrinsics`, vea la página de documentación [aquí](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-intrinsic-functions.html).

En esta sección, usará `States.MathAdd` para sumar dos números sin necesidad de usar una función Lambda para realizar la operación.
1. Vuelve a navegar a Workflow Studio para la máquina de estados `InputOutputProcessingMachine`.
2. Agrega un nuevo `Pass State` a la máquina de estados después del estado Lambda Invoke. Tenga en cuenta que no está limitado a ustilizar `Pass State` para `intrinsics`, podrá usarlos en cualquier estado que admita parámetros.

![Pass State Input](/static/img/module-6/pass-state-diagram.png)

3. En la pestaña `Input` del `Pass State`, complete el siguiente valor en el campo de texto del parámetro. Tenga en cuenta que deberá agregar el sufijo `.$` al usar intrínsecos.
    ```json
      {
        "Sum.$": "States.MathAdd($.value1, $.value2)"
      }
    ```

![Pass State Input](/static/img/module-6/pass-state-input-intrinsic.png)

4. A continuación salva  las modificaciones, haz clic en **Start execution** y use el JSON a continuación como entrada.
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
5. Una vez que la ejecución sea exitosa, revisa la salida en la pestaña `Execution input and output`. Verás que el campo sum tiene la suma de value1 y value2 de la entrada.

![Execution Output](/static/img/module-6/intrinsic-execution-output.png)

::alert[**Enhorabuena!** Usó una función intrínseca para realizar el procesamiento de datos básico sin necesidad de escribir código alguno!]{type="success"}