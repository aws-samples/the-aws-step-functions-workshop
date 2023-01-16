---
title: 'Limpieza'
weight: 98
---

:::alert{header="Important" type="warning"}
Siga las instrucciones de esta página si desea limpiar los recursos en su propia cuenta. Las cuentas de Event Engine no requieren limpieza.
:::

### Eliminar manualmente la máquina de estado

Navegue a **Step Function**
Si nombró las máquinas de estado según las instrucciones proporcionadas:

- Seleccione **ParallelProcessingMachine** de la lista de máquinas de estado.
- Haga clic en el botón **Delete**
- Confirme haciendo clic en el botón **Delete state machine** en el cuadro de diálogo que se muestra.
  ![Statemachine delete](/static/img/module-7/manual-delete-sm.png)

Si eligió diferentes nombres para su máquina de estado, siga las instrucciones anteriores seleccionando el nombre adecuado.

- Navegue a la página de [CloudFormation](https://console.aws.amazon.com/cloudformation/home) en la consola de AWS.
- Seleccione la pila con el nombre `SFW-Module-7` (o cualquier nombre que haya elegido para la pila) y luego haga clic en Eliminar.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Asegúrese de que la eliminación de la pila se complete con éxito.

### Eliminar manualmente el grupo de registros de CloudWatch

Navegue a [CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Haga clic en **Registros** en la navegación y seleccione **Grupos de registros**.

- seleccione el grupo de registros perteneciente a **ParallelProcessingMachine**.
- Haga clic en el desplegable **Acciones** y luego seleccione **Eliminar grupo(s) de registros**.
  ![Cloudwatch loggroup delete](/static/img/module-7/cloudwatch-cleanup.png)
- Confirme haciendo clic en el botón **Eliminar** en la pantalla emergente.

