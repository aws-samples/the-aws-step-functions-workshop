---
title: 'Revisión del impacto en los costos'
weight: 155

---

La optimización de costes es una razón clave para considerar la anidación de flujos de trabajo Express dentro de los flujos de trabajo Standard.

## Precios

|**Flujos de trabajo Estándar**|**Flujos de trabajo Express**|
---|---|
|Los flujos de trabajo Estándar se cobran en función del número de transiciones de estado necesarias para ejecutar una carga de trabajo. Step Functions cuenta una transición de estado cada vez que se ejecuta un paso de su flujo de trabajo. Se le cobra por el número total de transiciones de estado en todas sus máquinas de estado Estándar, incluyendo reintentos.|Los flujos de trabajo Express se cobran en función del número de veces que se ejecuta su máquina de estado y la duración. La duración se calcula desde el momento en que comienza a ejecutar el flujo de trabajo hasta que se completa o finaliza de otra manera, redondeada a la centena de milisengundo más próxima (100 ms), y la cantidad de memoria utilizada en la ejecución de su flujo de trabajo, facturada en bloques de 64 MB.|

## Comparación de precios

Mover los cuatro pasos de tareas Lambda de nuestro flujo de trabajo Estándar y reemplazarlos con un paso de ejecución de flujo de trabajo anidado Express elimina tres pasos de cada ejecución de máquina de estado.

Digamos que ejecutó el flujo de trabajo Estándar original 1000 veces en la región N. Virginia. Se le cobraría por 3000 transiciones de estado adicionales en comparación con el flujo de trabajo modificado.

### Flujo de trabajo original

**Costo total** = `(número de transiciones por ejecución x número de ejecuciones) x $0.000025`  
**Costo total** = `(3 X 1000) X 0.000025 = $0.075`  
(*Nota: esto no incluye las 4000 transiciones de estado incluidas en el AWS Free Tier cada mes*)  

### Flujo de trabajo Express anidado

En cambio, ahora se le cobra por el flujo de trabajo Express. Supongamos que cada invocación del flujo de trabajo Express tiene una duración promedio de 11300 ms y no utiliza más de 64 MB de memoria.  

**Costo de duración** = `(ms de duración facturados promedio / 100) * precio por 100 ms`  
**Costo de ejecución** = `$0.000001 por solicitud`  
**Costo total** = `(Costo de ejecución + Costo de duración) x Número de solicitudes`  

**Costo de duración** = `(11300 ms /100) * $ 0.0000001042 = $0.0000117746`  
**Costo de ejecución** = `$0.000001 por solicitud`  
**Costo total** = `($0.000001 + $0.0000117746) x 1000 = $0.01`  

Para resumir, en este ejemplo, cuesta 7.5 veces más mantener esos pasos en el flujo de trabajo Estándar. Al mover los pasos que no requieren las garantías de ejecución de un flujo de trabajo Estándar, a un flujo de trabajo anidado Express, se pueden obtener ahorros para su carga de trabajo.

## Cómo afecta la duración del flujo de trabajo Express al costo

Los ahorros de costos dependen del número de pasos que elimine de su flujo de trabajo Estándar y su duración. Si los pasos se ejecutan durante mucho tiempo (pero todavía dentro del límite de tiempo de cinco minutos para un flujo de trabajo Express), puede ser menos costoso dejarlos en el flujo de trabajo Estándar. En el ejemplo, eliminó tres transiciones de estado reemplazando cuatro pasos de tareas con un paso de flujo de trabajo anidado. El gráfico a continuación muestra el costo de 1000 ejecuciones de los tres pasos del flujo de trabajo Estándar, en comparación con el costo de los mismos pasos cuando se mueven a un flujo de trabajo Express anidado, variando la duración. Puede ver el rango de duraciones donde el flujo de trabajo Express anidado es menos costoso. Para obtener más información sobre el costo de los flujos de trabajo Estándar y Express, consulte la [Calculadora de precios de AWS](https://calculator.aws/).

![Cost comparison chart](/static/img/module-13/cost-comparison-by-duration.png)

## Conclusión

En este módulo, pudimos reducir el costo al mover pasos de un flujo de trabajo Estándar a un flujo de trabajo anidado de Express. Como se menciona [en la introducción](../), puede beneficiarse tanto en términos de ahorro de costos como de modularidad. Aquí hay otros ejemplos de algunas otras situaciones en las que puede querer anidar un flujo de trabajo dentro de otro:

1. Una máquina de estados que recupera datos de varias fuentes y realiza algunos pasos de preprocesamiento.
1. Un estado de tipo [Inline Map](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-asl-use-map-state-inline.html) que ejecuta varios pasos para cientos o miles de elementos.
1. Un subproceso propiedad de un equipo, que es utilizado por otros equipos. Por ejemplo, enviar una notificación a un cliente puede requerir recuperar su método de contacto preferido de un sistema CRM, verificar si han optado por ciertos tipos de mensajes, verificar las promociones aplicables, etc.
