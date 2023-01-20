---
title: 'Limpieza'
weight: 87
---
:::alert{header="Importante" type="warning"}
Siga las instrucciones en esta página si desea limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::


## Eliminar manualmente la máquina de estados

Navega hasta **Step Functions**. Si ha nombrado las máquinas de estado según las instrucciones proporcionadas:

- Seleccione **InputOutputProcessingMachine** de la lista de máquinas de estado.
- Haga clic en el botón **Delete**
- Confirme haciendo clic en el botón **Delete state machine** del cuadro de diálogo que aparece.
- Navegue a la página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en el Console de AWS.
- Seleccione la pila con el nombre `SFW-Module-6` (o cualquier nombre que haya elegido para la pila) y luego haga clic en Eliminar.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se complete con éxito.
