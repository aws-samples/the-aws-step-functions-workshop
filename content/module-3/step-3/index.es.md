---
title: 'Ejecutar tarea asíncrona'
weight: 53
---
Navega a [Step Functions en la consola](https://console.aws.amazon.com/states/home) y Haz clic en la máquina de estado que comienza con **"BatchJobNotification"**. Este flujo de trabajo envía un trabajo AWS Batch. En su estado inicial, el trabajo es asíncrono. La máquina de estado envía el trabajo al servicio AWS Batch pero no espera a que el trabajo se complete. En cambio, inmediatamente se mueve al siguiente estado y envía un mensaje de Notify Success a un tema de Amazon SNS.

Así es como se ve el flujo de trabajo inicial:

![Module 3 Workflow](/static/img/module-3/initial-workflow.png)

Así es como se ve la definición de tarea para el trabajo AWS Batch. Tome nota del campo "Resource".

![Module 3 Code](/static/img/module-3/initial-code.png)

Ahora Haz clic en **Iniciar ejecución** y use la entrada predeterminada. El servicio AWS Batch realiza un trabajo, que puede tardar un minuto o más en terminar. Observa cómo se completa rápidamente esta ejecución.

![Initial graph](/static/img/module-3/initial-graph.png)

Ahora imagine que necesitamos que nuestra máquina de estado se mantenga sincronizada con AWS Batch y solo continúe una vez que se haya completado el trabajo.
