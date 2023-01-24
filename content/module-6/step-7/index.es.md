---
title: 'Limpieza'
weight: 87
---
:::alert{header="Importante" type="warning"}
Sigue las instrucciones en esta página si deseas limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::


## Eliminar manualmente la máquina de estados

Navega hasta **Step Functions**. Si has nombrado las máquinas de estado según las instrucciones proporcionadas:

- Selecciona **InputOutputProcessingMachine** de la lista de máquinas de estado.
- Haz clic en el botón **Delete**
- Confirme haciendo clic en el botón **Delete state machine** del cuadro de diálogo que aparece.
- Navega a la página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en el Console de AWS.
- Selecciona la pila con el nombre `SFW-Module-6` (o cualquier nombre que haya elegido para la pila) y luego Haz clic en Eliminar.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se complete con éxito.
