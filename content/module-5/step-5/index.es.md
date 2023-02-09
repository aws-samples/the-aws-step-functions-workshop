---
title: 'Ejecuta la máquina de estados y revisa los resultados'
weight: 75
---

1. En la consola de [Step Functions](https://console.aws.amazon.com/states/home) , navega a **MapStateMachine** y da clic en **Start execution**. Tendrás que reemplazar el payload de ejecución por default. Expande `Payload de Ejecución`, copia y pega el JSON como tu payload de ejecución.
   ::::expand{header="Payload de Ejecución (Clic para expander)" defaultExpanded=false}
   :::code{showCopyAction=true showLineNumbers=false language=json}
   {
      "Data": [
         {
         "orderId": "1",
         "customerId": "1",
         "priority": "HIGH"
         },
         {
         "orderId": "2",
         "customerId": "2",
         "priority": "HIGH"
         },
         {
         "orderId": "3",
         "customerId": "3",
         "priority": "HIGH"
         },
         {
         "orderId": "4",
         "customerId": "4",
         "priority": "LOW"
         },
         {
         "orderId": "5",
         "customerId": "5",
         "priority": "HIGH"
         },
         {
         "orderId": "6",
         "customerId": "6",
         "priority": "LOW"
         },
         {
         "orderId": "7",
         "customerId": "7",
         "priority": "HIGH"
         }
      ]
   }
   :::
   ::::

2. La ejecución debe terminar después de unos segundos. Cuando la ejecución haya terminado, dirigete hacia las iteraciones del estado Map  en la **Table View**.
   1. Clic en el símbolo + de color gris para expander las iteraciones del estado Map.
   2. Expander las iteraciones #0 a la #2, #4, y #6 del estado Map muestra la máquina de estados seguida del path para elementos de prioridad `HIGH`, insertando los detalles de la orden en DynamoDB para aquellos elementos que se encuentran en el arreglo de entrada.
   3. Expander las iteraciones de #3 y #5 del estado Map muestra que la máquina de estados seguida por el path para elementos de prioridad `LOW`, que es un estado Success, detecta que los elementos son elementos de prioridad `LOW`. 
   4. La concurrencia máxima para el estado Map es de 1 iteración a la vez, lo que significa que procesaremos el arreglo de manera secuencia.. Justo después de que la primera iteración del mapa termine, la segunda comenzará, y así sucesivamente. Puedes revisar los detalles de la itración, duración y timestamps en las columnas Duration, Timeline, y Started After. En esta ejecución puedes ver como cada iteración del estado Map inició justo después de que la anterior termina. En el siguiente paso, demostraremos como actualizar tu máquina de estados para correr múltiples iteraciones de forma paralela. 
   5. También puedes revisar la tabla de [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) para ver si los items fueron puestos exitosamente dentro de la tabla **MapStateTable**.

![Vista de la tabla con 1 rama](/static/img/module-5/table-view-1-branch.png)

::alert[**Felicidades!** Aprendiste como usar estados Map y Choice en una máquina de estados]{type="success"}