---
title: 'Limpiar'
weight: 126
---

:::alerta{encabezado="Importante" tipo="warning"}
Sigue las instrucciones en esta página si deseas limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

### Destruir recursos creados por CDK

Cuando haya terminado de probar, puedes destruir la API REST de API Gateway y la máquina de estado utilizando AWS CDK. Copia/pega el siguiente comando en el terminal en el directorio raíz de la aplicación.

```bash
cdk destroy
```

Cuando se complete `cdk destroy`, verás el siguiente mensaje:
![CDK Destroy](/static/img/module-10/cdk-destroy.png)

### Eliminar pila de CloudFormation

- Navega a la página de [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en el console de AWS.
- Selecciona la pila con el nombre `SFW-Module-10` (o cualquier otro nombre que haya elegido para la pila) y luego Haz clic en Eliminar. Esto limpiará el entorno de AWS Cloud9 y cualquier otro recurso relacionado en la pila.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se complete con éxito.
