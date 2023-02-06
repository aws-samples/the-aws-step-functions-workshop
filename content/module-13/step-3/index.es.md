---
title: 'Resumen de la máquina de estado'
weight: 153
---

En su cuenta, tiene una máquina de estado con un nombre que comienza con _ParentStateMachine_. Actualmente, la máquina de estado es un flujo de trabajo Estándar. Como se mencionó al principio del módulo, esto puede ser necesario si su flujo de trabajo utiliza una característica solo disponible para los flujos de trabajo estándar, como la característica .waitForTaskToken o porque la duración del flujo de trabajo podría superar los cinco minutos o porque necesita un modelo de ejecución del tipo "exactamente una vez".

Sin embargo, tenga en cuenta los pasos marcados a continuación. Asumamos que estos pasos son idempotentes y serían adecuados en un modelo de ejecución "al menos una vez", como el que proporcionan los flujos de trabajo Express. Podríamos mover esos pasos a un flujo de trabajo anidado Express.

![Pasos que podrían moverse a un flujo de trabajo Express](/static/img/module-13/state-machine-express-step-candidates.png)

