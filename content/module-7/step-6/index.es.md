---
title: 'Ejecutar una ejecución síncrona a través de API Gateway'
weight: 96
---

## Haz la integración síncrona

1. Ve al panel de control de API Gateway y selecciona la API creada para este módulo.
   ![API Console](/static/img/module-7/api-console-4.png)
2. De la lista de recursos, encuentra el recurso `ejecución` y haz clic en `POST`
   ![API Execution](/static/img/module-7/api-execution-new-4.png)
3. Haz clic en `Solicitud de integración`
4. Edita la `Acción` haciendo clic en el lápiz gris y cámbiala por `StartSyncExecution`, luego haz clic en el botón de actualizar (marca de verificación gris)
   ![API Execution Sync](/static/img/module-7/api-integration-setup-sync.png)
5. Vuelve a probar tu API.
6. Notarás un cuerpo de respuesta más grande con más detalles de la ejecución de la máquina de estado, incluyendo la `input` y la `output`
   ![API Test Result Sync](/static/img/module-7/api-test-result-sync-4.png)

::alert[**¡Felicidades!** Acabas de ejecutar una integración síncrona entre API Gateway y Step Functions.]{type="success"}
