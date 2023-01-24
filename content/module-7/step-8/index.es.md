---
title: 'Limpieza'
weight: 98
---

:::alert{header="Importante" type="warning"}
Sigue las instrucciones de esta página si deseas limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

### Eliminar manualmente la máquina de estado

Navega a **Step Function**
Si nombró las máquinas de estado según las instrucciones proporcionadas:

- Selecciona **ParallelProcessingMachine** de la lista de máquinas de estado.
- Haz clic en el botón **Delete**
- Confirme haciendo clic en el botón **Delete state machine** en el cuadro de diálogo que se muestra.
  ![Statemachine delete](/static/img/module-7/manual-delete-sm.png)

Si eligió diferentes nombres para su máquina de estado, sigue las instrucciones anteriores seleccionando el nombre adecuado.

- Navega a la página de [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en la consola de AWS.
- Selecciona la pila con el nombre `SFW-Module-7` (o cualquier nombre que haya elegido para la pila) y luego Haz clic en Eliminar.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se complete con éxito.

### Eliminar manualmente el grupo de registros de CloudWatch

Navega a [CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Haz clic en **Registros** en la navegación y selecciona **Grupos de registros**.

- selecciona el grupo de registros perteneciente a **ParallelProcessingMachine**.
- Haz clic en el desplegable **Acciones** y luego selecciona **Eliminar grupo(s) de registros**.
  ![Cloudwatch loggroup delete](/static/img/module-7/cloudwatch-cleanup.png)
- Confirme haciendo clic en el botón **Eliminar** en la pantalla emergente.

