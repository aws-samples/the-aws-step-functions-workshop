---
title: 'Probar el proyecto'
weight: 125
---

Después de crear tu API Gateway REST integrando la máquina de estado Express síncrona como back-end, puedes probar la API.

### Probar el API Gateway desplegado utilizando la consola de API Gateway

1. Abre la [consola de Amazon API Gateway](https://console.aws.amazon.com/apigateway/) e inicia sesión.
2. Elige tu API REST llamada, `CDKStepFunctionsRestApi`.
3. En el panel **Recursos**, puedes seleccionar el método que deseas probar. Haz clic en el método `ANY`.
   ![API GAteway ANY](/static/img/module-10/api-gateway-testing.png)
4. En el panel **Ejecución del método**, en el cuadro **Cliente**, elige **Prueba**.
5. Elige **POST** en el menú desplegable **Método**. Copia y pega el JSON de abajo en el campo **Cuerpo de la solicitud**.
   :::code{showCopyAction=true showLineNumbers=true language=json}
   {
   "key": "Hello Step Functions!"
   }
   :::
6. Haz clic en **Prueba**. Se mostrará la siguiente información:

- **Solicitud** es la ruta del recurso que se llamó para el método.
- **Estado** es el código de estado HTTP de la respuesta.
- **Latencia** es el tiempo desde la recepción de la solicitud y la respuesta devuelta.
- **Cuerpo de la respuesta** es el cuerpo de la respuesta HTTP.
- **Encabezados de respuesta** son los encabezados de respuesta HTTP.
- **Registros** son las entradas simuladas de Amazon CloudWatch Logs que se habrían escrito si este método se hubiera llamado fuera de la consola de API Gateway.
  ::alert[Aunque las entradas de CloudWatch Logs son simuladas, los resultados de la llamada al método son reales.]{header="Nota"}

La salida de **Cuerpo de respuesta** debería ser:

```bash
"Hello back to you!"
```

### Prueba la API desplegada usando cURL

- Abre una nueva ventana de terminal en tu entorno AWS Cloud9.
- Copia el siguiente comando cURL y pégalo en la ventana de terminal, reemplazando `<api-id>` con el ID de la API REST de API Gateway y `<region>` con la región donde se ha desplegado tu API. Es posible que hayas copiado esta URL desde la salida de CloudFormation en el último paso. También puedes encontrar la URL completa de invocación en la consola de API Gateway navegando a **Etapas > prod**.

```bash
curl -X POST\
 'https://<api-id>.execute-api.<region>.amazonaws.com/prod' \
 -d '{"key":"Hello Step Functions"}' \
 -H 'Content-Type: application/json'
```

La respuesta debería ser:

```bash
"Hello back to you!"
```

::alert[**¡Enhorabuena!** Has completado este módulo.]{type="success"}
