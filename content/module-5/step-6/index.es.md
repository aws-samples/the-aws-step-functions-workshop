---
title: 'Aumenta la concurrencia del estado Map y corre el flujo nuevamente'
weight: 76
---
1. Haz clic en  **Edit State Machine** en la parte superior derecha.
![EDITAR](/static/img/module-5/edit-state-machine.png)

2. Abre la máquina de estados con el nombre **MapStateStateMachine** en Workflow Studio haciendo clic en el botón Workflow en la parte derecha de la pantalla.

![EDITAR](/static/img/module-5/workflow-studio-button.png)

Si ves la siguiente imagen, estás en el lugar correcto.

![EDITAR](/static/img/module-5/module5-workflowstudio.png)

3. Actualiza la máquina de estados para aumentar el valor de máxima concurencia para el estado `Map`. Expande el siguiente sección para ver como actualizar la opción, o sigue las siguientes instrucciones.
   1. Haz clic en el estado `Map` en el canvas de Workflow Strudio.
   2. Baja en el pestaña de configuración hasta que veas la opción de `Maximum concurrency`.
   3. Actualiza el valor a 2 iteraciones paralelas.
   4. Esto significa que nuestro estado `Map` procesara hasta 2 elementos de manera paralela del arreglo de entrada. Aumentando el número de iteraciones paralelas nos permite procesar datasets de mayor tamaño en un menor tiempo a comparación de procesar cada elemento de forma secuencial
   5. Guarda tus cambios de la máquina de estados utilizando el botón `Apply and exit`.

::::expand{header="Panel de Configuraicón del estado Map (Clic para expandir)" defaultExpanded=false}
![EDITAR](/static/img/module-5/map-state-configuration-parallel.png)
::::

1. Inicia una nueva ejecución de la máquina de estados con el mismo payload de la ejecución pasada.

   ::::expand{header=" Payload de ejecución (Clic para expandir)" defaultExpanded=false}
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

2. La ejecución debería terminar después de unos segundos. Cuando la ejecución termine, dirígete a la iteración en la sección de **Table View**.
   1. Las iteraciones tendran del mismo resultado de procesamiento con elementos `HIGH` y `LOW` .
   2. Podemos ver nuestras iteraciones en paralelo en acción fijándonos en las columnas Timeline y Started After.
   3. Iteración #0 e iteración #1 inicializaron al mismo tiempo.
   4. Cuando la iteración #0 concluya, Iteración #2 inicia. El estado `Map` crea ramas nuevas del flujo de trabajo cada vez que un flujo anterior es completado, sin esperar que todas las ramas actuales del flujo de trabajo concluyan. Aunque la iteración #1 no haya concluido, el estado `Map` ya ha iniciado la iteración #2.
   5. Cuando la iteración #1 termina, Iteración #3 inicia.
   6. Iteración #3 no inserta un elemento en la tabla de DynamoDB, así que su duración es muy corta.
   7. Cuando la iteración #3 termina, la iteración #4 inicia.

En términos de tiempo de procesamiento total, esta ejecución tomo a penas la mitad del tiempo que la ejecución con una sola iteración en paralelo. Esto es por que la máquina de estados de Step Functions no estaba restringida al procesamiento de un elemento a la vez y esperar que cada elemento con prioridad  `HIGH` terminara de escribir en la tabla de DynamoDB, antes de inicializar el procesamiento del siguiente elemento.

![Vista de la tabla con  2 ramas en paralelo](/static/img/module-5/table-view-2-parallel.png)

::alert[**¡Enhorabuena!** Tomaste ventaja de la concurrencia del estado Map para aumentar la velocidad del procesamiento de datos.]{type="success"}
