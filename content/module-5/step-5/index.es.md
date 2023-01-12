---
title: 'Ejecuta la máquina de estados y revisa los resultados'
weight: 75
---

1. **Suscríbase al tema de Amazon SNS (opcional)**

 - Abra la [consola de Amazon SNS](https://console.aws.amazon.com/sns/home).

 - Haga clic para ver los temas 
 
 - Haga clic en el tema **MapStateTopicForMessages**

 - En Suscripciones, selecciona Crear suscripción.

 - Verás la página Crear suscripción, en la que se muestra el ARN del tema.

 - En Protocolo, selecciona Correo electrónico.

 - En Punto de enlace, introduce tu dirección de correo electrónico.

 - Selecciona Crear suscripción.

 - Abre la confirmación de suscripción enviada a tu dirección de correo electrónico y haz clic en el enlace `Confirm subscription`.

:::alert{header="Note" type="warning"}
Debe confirmarlo haciendo clic en el enlace enviado por correo electrónico para que la suscripción esté activa.
:::

![SNS](/static/img/module-5/sns-subscription.png)

2. **Añadir mensajes a la cola de Amazon SQS**

 - Abra la [consola de Amazon SQS](https://console.aws.amazon.com/sqs/home).

 - Haga clic en la cola **MapStateQueueForMessages**.

 - Haz clic en el botón **Enviar y recibir mensajes**.

 - En la ventana Enviar mensaje, introduzca un mensaje y pulse **Enviar mensaje**.

 - Sigue enviando mensajes hasta que tengas muchos en la cola.

:::alert{header="Note type="info"}
Con solo unos pocos elementos en la cola, la acción SQS ReceiveMessage a veces puede devolver solo un mensaje. Para aumentar tus posibilidades de recuperar y procesar varios mensajes, añade más mensajes a la cola. 
:::

![SQS](/static/img/module-5/sqs-send-message.png)

3. Regrese a [Step Functions](https://console.aws.amazon.com/states/home). Haga clic en **MapStateMachine** y **Start execution**. Copia y pega el JSON de abajo como carga de entrada.
   :::code{showCopyAction=true showLineNumbers=false language=json}
   { "Comment": "Testing Map & Choice states" }
   :::

4. Cuando se complete una ejecución, seleccione algunos de los estados del **Graph View** y consulte sus valores **Input** y **Output**. Si creaste una suscripción por correo electrónico, deberías recibir mensajes de correo electrónico. También puede consultar la tabla [DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) para ver si los elementos se han insertado correctamente en **MapStateTable**.

![DDB](/static/img/module-5/ddb-map-state.png)

::alert[**¡Enhorabuena!** Ha ejecutado una máquina de estados utilizando los estados Map y Choice.]{type="success"}
