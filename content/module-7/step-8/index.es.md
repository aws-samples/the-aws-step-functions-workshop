---
title: 'Limpieza'
weight: 98
---

:::alert{header="Importante" type="warning"}
Sigue las instrucciones de esta página si deseas limpiar los recursos en tu propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

### Eliminar manualmente la máquina de estado

Navega a **Step Function**
Si nombraste la máquina de estado según las instrucciones proporcionadas:

- Selecciona **ParallelProcessingMachine** de la lista de máquinas de estado.
- Haz clic en el botón **Delete**
- Confirma haciendo clic en el botón **Delete state machine** en el cuadro de diálogo que se muestra.
  ![Statemachine delete](/static/img/module-7/manual-delete-sm.png)

Si eligiste un nombre diferente para tu máquina de estado, sigue las instrucciones anteriores seleccionando el nombre adecuado.

- Navega a la página de [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en la consola de AWS.
- Selecciona la pila con el nombre `SFW-Module-7` (o cualquier nombre que hayas elegido para la pila) y luego haz clic en **Eliminar**.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrate de que la eliminación de la pila se complete con éxito.

### Eliminar manualmente el grupo de registros de Amazon CloudWatch

Navega a [Amazon CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Haz clic en **Registros** en la navegación y selecciona **Grupos de registros**.

- Selecciona el grupo de registros perteneciente a **ParallelProcessingMachine**.
- Haz clic en el desplegable **Acciones** y luego selecciona **Eliminar grupo(s) de registros**.
  ![Cloudwatch loggroup delete](/static/img/module-7/cloudwatch-cleanup.png)
- Confirma haciendo clic en el botón **Eliminar** en la pantalla emergente.
