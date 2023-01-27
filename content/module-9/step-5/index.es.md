---
title: 'Limpieza'
weight: 115
---

:::alert{header="Importante" type="warning"}
Sigue las instrucciones en esta página si deseas limpiar los recursos en tu propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

## Eliminar manualmente la máquina de estado

Navega a **Step Functions**
Si nombró las máquinas de estado según las instrucciones proporcionadas:

- Selecciona **DetectSentimentMachine** de la lista de máquinas de estado.
- Haz clic en el botón **Delete**
- Confirme haciendo clic en el botón **Delete state machine** en el cuadro de diálogo que se muestra.

- Navega a la página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en la consola de AWS.
- Selecciona la pila con el nombre `SFW-Module-9` (o cualquier nombre que hayas elegido para la pila) y luego haz clic en **Eliminar**.
  ![CloudFormation delete](/static/img/es/setup/setup-cloudformation-delete.png)
- Asegúrate de que la eliminación de la pila se complete con éxito.

