---
title: 'Clean up'
weight: 136
---

::alert{header="Important" type="warning"}
Siga las instrucciones en esta página si desea limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

### Destruir los recursos creados por SAM

Cuando haya terminado de probar, puede destruir la API y la máquina de estado utilizando AWS SAM. Copie / pegue el siguiente comando en el terminal en el directorio raíz de la aplicación.

```bash
sam delete
```

Cuando se complete `sam delete` verá el siguiente mensaje:
![SAM Delete](/static/img/module-11/sam-delete.png)

### Eliminar la pila de CloudFormation

- Navegue a la página de [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en el AWS Console.
- Seleccione la pila con el nombre `SFW-Module-11` (o cualquier nombre que haya elegido para la pila) y luego haga clic en Eliminar. Esto limpiará el entorno de AWS Cloud9 y cualquier otro recurso relacionado en la pila.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se completa con éxito.
