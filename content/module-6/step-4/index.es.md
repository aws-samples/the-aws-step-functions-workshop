---
title: 'Ejecutar la máquina de estados y revisar los resultados'
weight: 84
---

1. Haga clic en la máquina de estados `InputOutputProcessingMachine` desde la consola de Step Functions.
2. Haga clic en **Start execution** y utilice el JSON a continuación como su carga de entrada.
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
3. Una vez que la ejecución sea exitosa, revise la salida en la pestaña `Execution input and output`. Observe cómo el bloque de datos en el json de entrada se agrega a la salida de la función Lambda. Esta salida se pasaría al siguiente estado en su flujo de trabajo.

::alert[**¡Enhorabuena!** Ha ejecutado una máquina de estados utilizando las características de procesamiento de datos de entrada y salida.]{type="success"}

