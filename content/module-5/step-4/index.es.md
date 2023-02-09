---
title: 'Localiza tus recursos y configura tu máquina de estados'
weight: 74
---

### Localiza tus recursos

Navega a los servicios en la consola para familiarizarte con los recursos. Asegúrate que te encuentres en la región correta. Copia el ARN (Amazon Resource Name) del tópico de SNS a un bloc de notas.
Lo necesitarás más adelante en el módulo. 

1. Navega a [Step Functions](https://console.aws.amazon.com/states/home) en la consola de AWS.

### Observa tu máquina de estados

1. Navega a [Step Functions](https://console.aws.amazon.com/states/home) en la consola de AWS.

2. Localiza la máquina de estados que contenga **MapStateStateMachine** en su nombre. Da clic en ella y luego en **Edit** en la esquina superior derecha.

![EDIT](/static/img/module-5/map-state-definition-edit.png)

3. Abre **MapStateStateMachine** en Workflow Studio dando clic en el botón de Workflow Studio del lado derecho de la pantalla.
![EDIT](/static/img/module-5/workflow-studio-button.png)

![EDIT](/static/img/module-5/module5-workflowstudio.png)

4. Da clic en el estado `Map` `Iteration Over Input Array` y revisa los detalles de la configuración.
   1.  **Processing mode: Inline** - Este es la forma de procesar entradas relativamente pequeñas y fuentes de datos. Si quieres aprender más de como procesar datasets más grandes tales como aquellos que se encuentren en S3, revisa el módulo de Mapas Distribuidos más adelante en este workshop!
   2.  **Fuente de los elementos - Provee un path de los items del arreglo** - Esta configuración se utiliza para apuntar el estado `Map` al arreglo específico del JSON de entrada.
   3.  **Concurrencia Máxima** - Esta configuración se utiliza para definir cuantos elementos queremos procesar de manera paralela. El default es 0, lo que significa que procesaremos los datos secuencialmente, un elemento a la vez. Exploraremos esta configuración en este módulo.
   ::::expand{header="Configuración del estado `Map` (Clic para expandir)" defaultExpanded=false}
  ![Configuración del estado Map](/static/img/module-5/map-state-configuration.png)
  ::::
1. Selecciona el estado `Choice` `Priority Filter` y observa las reglas de selección que fueron definidas en la máquina de estados.
   1. **Regla #1**: $.priority == `LOW`. Dado cada elemento del arreglo, revisaremos el valor de la prioridad, y Step Functions enrutará el elemento al estado definido para ese path. En este caso, los elementos de prioridad baja`LOW` son enrutados al estado de éxito `Low Priority Order Detected`, estos no serán guardados en la tabla de DynamoDB.
   2. **Regla #2**: $.priority == `HIGH`. En este caso, los elementos con prioridad alta `HIGH` se enrutarán a `Insert High Priority Order` y serán guardado en la tabla de DynamoDB.
   3. Cuando trabajes con el estado `Choice` en tu máquina de estado, utiliza Workshop Studio y haz clic en el botón `Add new choice rule` para comenzar a construir de manera rápida la lógica necesaria para enrutar tus datos. 
  ::::expand{header="Configuración del estado `Choice` (Clic para expandir)" defaultExpanded=false}
  ![Choice State Configuration](/static/img/module-5/choice-state-configuration.png)
  ::::