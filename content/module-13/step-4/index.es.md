---
title: 'Reemplazar pasos con un flujo de trabajo Express anidado'
weight: 154
---

Reemplacemos los pasos en nuestro flujo de trabajo Estándar con un flujo de trabajo Express anidado. Un flujo de trabajo Express que contiene estos pasos ya se ha creado en su cuenta, con un nombre que comienza con _ChildStateMachine_.

1. En la [Consola de Step Functions](https://console.aws.amazon.com/states/home), seleccione **State machines** en el lado izquierdo y luego haga clic en la máquina de estado con el nombre que comienza con *ChildStateMachine*. Desde el cuadro "Details" en la parte superior, copie el valor ARN, ya que lo usará en un paso posterior.  

2. A continuación, abra la máquina de estado con el nombre que comienza con *ParentStateMachine*. Haga clic en `Edit` y luego haga clic en el botón Workflow Studio en el lado derecho para editar la máquina de estado en Workflow Studio.  

3. Comience eliminando los pasos **Update Order History**, **Update Data Warehouse**, **Update Customer Profile** y **Update Inventory** seleccionando los pasos y haciendo clic en **Delete all selected states**.  

    ![Delete existing workflow steps](/static/img/module-13/delete-steps-from-workflow.png)

4. Ahora, agregue un paso StartExecution de AWS Step Functions, entre **Notify Payment Success** y **Ship the Package** arrastrando desde la paleta en la izquierda. Si StartExecution no está disponible en la sección "Más populares", escriba StartExecution en la barra de búsqueda en la parte superior de la paleta.  

    ![Add StartExecution step](/static/img/module-13/add-start-execution-step.png)

5. Haga clic en el paso **Step Functions StartExecution** que acaba de agregar para configurarlo para invocar el flujo de trabajo Express. Para dejar claro lo que hace este flujo de trabajo anidado, actualice el "State name" a "Workflow to Update Backend Systems".  

6. A continuación, en el cuadro "API Parameters", reemplace el valor del atributo "StateMachineArn" con el ARN que copió en el paso 1. Esto le dice a Step Functions qué flujo de trabajo anidado ejecutar. También puede eliminar opcionalmente el atributo "StatePayload", ya que no se utiliza en el flujo de trabajo anidado.  

    ![Configure nested Express workflow](/static/img/module-13/configure-nested-express-workflow.png)

7. Cuando hayas realizado las actualizaciones, haz clic en el botón **Apply and exit** y luego en el botón **Save**.

8. Es posible que recibas una advertencia de que los cambios podrían afectar a los recursos que tu máquina de estado necesita acceder y, por lo tanto, pueden ser necesarias actualizaciones en el rol de IAM utilizado por tu máquina de estado. Por simplicidad, el rol ya contiene los permisos necesarios, pero en el mundo real, debes asegurarte de revisar el rol de IAM utilizado por tu máquina de estado.

9. Ejecuta la máquina de estado actualizada haciendo clic en el botón **Start execution** en la esquina superior derecha. La máquina de estado no requiere ninguna entrada, puedes dejar el atributo "Comment" que se incluye por defecto, si lo deseas. Haz clic en **Start execution**. Ahora puedes ver la máquina de estado mientras se ejecutan los pasos y deberías ver un diagrama completamente verde. Ahora, haz clic en el enlace **State machines** en el lado izquierdo y elige el flujo de trabajo que comienza con _ChildStateMachine_. En la pestaña **Monitoring**, deberías ver un valor de 1 para la métrica **Executions Started** y un valor de 1 para la métrica **Executions Succeeded**, lo que indica que el flujo de trabajo anidado se ejecutó con éxito.

    ![Child Express workflow execution stats](/static/img/module-13/child-state-machine-execution-stats.png)

::alert[**¡Enhorabuena!** Reemplazaste varios pasos de flujo de trabajo Estándar con un flujo de trabajo anidado de Express]{type="success"}
