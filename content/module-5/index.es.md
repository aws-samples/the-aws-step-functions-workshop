---
title: 'Módulo 5 - Estado Choice y estado Map'
weight: 70
---

## Estado Choice

El estado [Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) agrega lógica de ramificación a una máquina de estados. Además de la mayoría de los campos de estado comunes, los estados de `Choice` contienen los siguientes campos adicionales:

- Choices (Obligatorio) - una matriz de reglas de elección que determina a qué estado la máquina de estados pasa después.

- Default (Opcional, recomendado) - el nombre del estado al que se transiciona si ninguna de las transiciones en Elecciones se toma.

## Estado Map

El estado [Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) puede ejecutar un conjunto de pasos paralelos para cada elemento de una matriz de entrada. Para configurar un estado `Map`, define un `Iterator`, que es un subflujo de trabajo completo. Cuando una ejecución de Step Functions ingresa a un estado `Map`, iterará sobre una matriz JSON en la entrada del estado. Para cada elemento, el estado `Map` ejecutará un subflujo de trabajo, posiblemente en paralelo. Cuando se completen todas las ejecuciones de subflujos de trabajo, el estado `Map` devolverá una matriz que contiene la salida para cada elemento procesado por el Iterador.

**Duración estimada: 20 minutos**
