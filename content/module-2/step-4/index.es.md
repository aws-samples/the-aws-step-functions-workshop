---
title: 'Iniciar ejecución'
weight: 44
---

Ahora ve adelante y haz clic en "Start execution" en esta máquina de estado utilizando los siguientes valores de entrada:

::code[{ "message": "¡Bienvenido a re:Invent!", "timer_seconds": 5 }]{showCopyAction=true language="js"}

Navega al historial de eventos de ejecución para esta ejecución. Notará que el tiempo de ejecución para la tarea `"Send SNS Task"` es relativamente rápido. La máquina de estado continúa tan pronto como se llama a la API Publicar SNS.

![Module 2 Result](/static/img/module-2/results.png)

En este caso, la tarea `"Send SNS Task"` se completó en 120ms. Revisa su propio historial de eventos de ejecución para comparar resultados.

::alert[**¡Enhorabuena!** Has ejecutado una máquina de estado utilizando el patrón de respuesta de la solicitud.]{type="success"}
