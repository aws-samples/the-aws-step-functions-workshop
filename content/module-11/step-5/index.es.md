---
title: 'Probando el proyecto'
weight: 135
---

Después de crear tu API REST integrando una máquina de estados Express síncrona como backend, puedes probar la API.

### Prueba el API Gateway implementado usando la consola de API Gateway

1. Abre la [consola de Amazon API Gateway](https://console.aws.amazon.com/apigateway/) e inicia sesión.
2. Elige tu REST API llamada, `SAMStepFunctionsRestApi`.
3. En el panel **Recursos**, puedes seleccionar el método que deseas probar. Haz clic en el método `POST`.
   ![API Gateway POST](/static/img/module-11/api-gateway-testing.png)
4. En el panel **Ejecución del método**, en el cuadro **Cliente**, elige **PRUEBA**.
5. Copia y pega el JSON de abajo en el campo **Cuerpo de la solicitud**.
   :::code{showCopyAction=true showLineNumbers=true language=json}
   {
   "key": "Hello Step Functions!"
   }
   :::
6. Haz clic en **Probar**. Se mostrará la siguiente información:

- **Solicitud** es la ruta del recurso que se llamó para el método.
- **Estado** es el código de estado HTTP de la respuesta.
- **Latencia** es el tiempo desde la recepción de la solicitud y la respuesta devuelta.
- **Cuerpo de la respuesta** es el cuerpo de la respuesta HTTP.
- **Encabezados de respuesta** son los encabezados de respuesta HTTP.
- **Registros** son las entradas simuladas de Amazon Amazon CloudWatch Logs que se habrían escrito si este método se hubiera llamado fuera de la consola de API Gateway.
  ::alert[Aunque las entradas de CloudWatch Logs son simuladas, los resultados de la llamada al método son reales.]{header="Nota"}

La salida de **Cuerpo de respuesta** debería ser:

```bash
"Hello back to you!"
```

### Prueba la API desplegada usando cURL

- Abre una nueva ventana de terminal en tu entorno AWS Cloud9.
- Copia el siguiente comando cURL y pégalo en la ventana de terminal, reemplazando `<api-id>` con el ID de la API REST de API Gateway y `<region>` con la región donde se ha desplegado tu API. Es posible que hayas copiado esta URL desde la salida de CloudFormation en el último paso. También puedes encontrar la URL completa de invocación en la consola de API Gateway navegando a **Etapas > dev**.

```bash
curl -X POST\
 'https://<api-id>.execute-api.<region>.amazonaws.com/dev' \
 -d '{"key":"Hello Step Functions"}' \
 -H 'Content-Type: application/json'
```

La respuesta debería ser:

```bash
"Hello back to you!"
```

::alert[¡Enhorabuena! Has completado con éxito este módulo.]{type="success"}
