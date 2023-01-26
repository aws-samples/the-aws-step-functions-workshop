---
title: 'Ejecutar una ejecución asíncrona a través de la API Gateway'
weight: 95
---

1. Ve a la consola de la API Gateway y selecciona la API creada para este módulo.
   ![API Console](/static/img/module-7/api-console-3.png)
2. De la lista de recursos, encuentra el recurso `execution` y Haz clic en `POST`
   ![API Execution New](/static/img/module-7/api-execution-new.png)
3. Haz clic en `Prueba`
4. En la parte inferior de la página encontrarás un campo llamado `Cuerpo de la solicitud`, pega allí el siguiente json y reemplaza el ejemplo `stateMachineArn` con el ARN de su máquina de estado.
:::code{showCopyAction=true language=json}
{
"input": "{\"data\": [20,40,60,10,9]}",
"name": "MyExecution",
"stateMachineArn": "arn:aws:states:us-east-1:123456789012:stateMachine:ParallelProcessingMachine"
}
:::
   ![Prueba de la API](/static/img/module-7/api-test.png)
5. Haz clic en `Pruebas`.  
6. Mira el `Cuerpo de la respuesta`. Observa que incluye referencias al `executionArn` y la `fecha de inicio`. Estas respuestas se devuelven porque la máquina de estado se ejecutó de forma asíncrona.
   ![Resultado de la prueba de la API](/static/img/module-7/api-test-result.png)

::alert[**¡Enhorabuena!** Acabas de ejecutar una integración asíncrona entre la API Gateway y las funciones Step.]{type="success"}

