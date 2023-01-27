---
title: 'Implementar devolución de llamada'
weight: 65
---

Navega al [servicio Lambda en la consola](https://console.aws.amazon.com/lambda/home) y encuentra la función que contiene la cadena **CallbackWithTaskToken**. Esta es la función que se encarga de procesar los mensajes agregados a la cola SQS. Modificarás esta función para implementar una devolución de llamada.

Revisa el código y observa que la función Lambda recibe el `TaskToken` de SQS y puede devolverlo a la máquina de estado como un parámetro en el método `.sendTaskSuccess`.

Descomenta el código indicado en la imagen a continuación y haz clic en el botón **Deploy**.

![Module 4 Workflow](/static/img/module-4/lambda.png)
