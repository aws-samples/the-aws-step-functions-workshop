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

