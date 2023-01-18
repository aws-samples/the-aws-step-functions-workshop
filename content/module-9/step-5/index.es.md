---
title: 'Limpieza'
weight: 115
---

:::alert{header="Important" type="warning"}
Siga las instrucciones en esta página si desea limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

## Eliminar manualmente la máquina de estado

Navegue a **Step Functions**
Si nombró las máquinas de estado según las instrucciones proporcionadas:

- Seleccione **DetectSentimentMachine** de la lista de máquinas de estado.
- Haga clic en el botón **Delete**
- Confirme haciendo clic en el botón **Delete state machine** en el cuadro de diálogo que se muestra.

- Navegue a la página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en la consola de AWS.
- Seleccione la pila con el nombre `SFW-Module-9` (o cualquier nombre que haya elegido para la pila) y luego haga clic en **Eliminar**.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se complete con éxito.

