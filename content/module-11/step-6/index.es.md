---
title: 'Clean up'
weight: 136
---

:::alert{header="Importante" type="warning"}
Sigue las instrucciones en esta página si deseas limpiar los recursos en tu propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

### Destruir los recursos creados por SAM

Cuando hayas terminado de probar, puedes destruir la API y la máquina de estado utilizando AWS SAM. Copia y pega el siguiente comando en el terminal en el directorio raíz de la aplicación.

```bash
sam delete
```

Cuando se complete `sam delete` verás el siguiente mensaje:
![SAM Delete](/static/img/module-11/sam-delete.png)

### Eliminar la pila de CloudFormation

- Navega a la página de [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en la consola de AWS.
- Selecciona la pila con el nombre `SFW-Module-11` () y luego haz clic en `Eliminar`. Esto limpiará el entorno de AWS Cloud9 y cualquier otro recurso relacionado en la pila.
  ![CloudFormation delete](/static/img/es/setup/setup-cloudformation-delete.png)
- Asegúrate de que la eliminación de la pila se complete con éxito.
