---
title: 'Resumen de la máquina de estado'
weight: 153
---

En tu cuenta, tienes una máquina de estado con un nombre que comienza con _ParentStateMachine_. Actualmente, la máquina de estado es un flujo de trabajo Estándar. Como se mencionó al principio del módulo, esto puede ser necesario si tu flujo de trabajo utiliza una característica solo disponible para los flujos de trabajo Estándar, como la característica `.waitForTaskToken` o porque la duración del flujo de trabajo podría superar los cinco minutos o porque necesitas un modelo de ejecución del tipo "exactamente una vez".

Sin embargo, ten en cuenta los pasos marcados a continuación. Asumamos que estos pasos son idempotentes y serían adecuados en un modelo de ejecución "al menos una vez", como el que proporcionan los flujos de trabajo Express. Podríamos mover esos pasos a un flujo de trabajo Express anidado.

![Steps that could move to an Express workflow](/static/img/module-13/state-machine-express-step-candidates.png)
