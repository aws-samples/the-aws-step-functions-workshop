---
title: 'Usar Workflow Studio para construir una máquina de estados'
weight: 83
---

1. Navegue a [Step Functions](https://console.aws.amazon.com/states/home) en su consola de AWS. Asegúrese de estar en la región de AWS correcta.

2. Haga clic en el botón **Create state machine**.

3. Para `Elegir método de autoría` seleccione **Design your workflow visually**, seleccione el tipo de máquina de estado `Tipo` como **Standard** y haga clic en **Next**.
   ![Studio](/static/img/module-6/studio-selection.png)

4. Debería ver el Workflow Studio ahora.
   ![Studio Designer](/static/img/module-6/studio-designer.png)

5. Ingrese un `Comentario` en el lado derecho: 

```bash
Un ejemplo de funciones de paso que muestra el procesamiento de entrada y salida.
```

6. Arrastre y suelte la acción **AWS Lambda Invoke** de la sección `Actions` en el lado izquierdo en el formulario del diseñador donde dice `Drag first state here`.
   ![Lambda Invoke](/static/img/module-6/lambda-invoke-state.png)

7. Configure el estado.

- En la pestaña `Configuración` del diseñador, ingrese un nombre para este estado: `Invoke HelloFunction`.
- Debería tener una función Lambda llamada `HelloFunction` ya implementada en su cuenta.
- Configure este estado para invocar esa función. Encuentre el campo `Parámetros de la API` y haga clic en `Ingresar nombre de función`. Desplácese por la lista de menú hasta encontrar **HelloFunction:$LATEST**. Seleccione este valor.

![Configuration](/static/img/module-6/configuration.png)

- Haga clic en la pestaña `Input` y marque la casilla para `Filter input with InputPath - optional`. Ingrese `$.lambda` para el valor.
  ![Config Input](/static/img/module-6/config-input.png)
- Haga clic en la pestaña `Output` y marque la casilla para `Add original input to output using ResultPath - optional`. Seleccione `Combine original input with result`. Ingrese la siguiente cadena como el filtro ResultPath: `$.data.lambdaresult`.
- Marque la casilla para `Filter output with OutputPath` e ingrese `$.data` para el valor.
  ![Config Output](/static/img/module-6/config-output.png)
- Haga clic en la pestaña `Error handling`. Encuentre la sección **Retry on errors** y elimine el `Retrier #1` predeterminado haciendo clic en el icono de edición a la derecha y desplazándose hacia abajo para hacer clic en el botón **Remove**.
  ![Remove Retrier](/static/img/module-6/remove-retrier.png)
- Haga clic en **Next** y revise el código generado y haga clic en **Next** nuevamente.
- Ingrese el nombre de la máquina de estados: `InputOutputProcessingMachine`. Para el rol de ejecución, elija un rol existente: `InputOutputProcessingStepFunctionRole`
  ![Iam Role](/static/img/module-6/name-iam-role.png)
- Deje los valores predeterminados restantes y haga clic en **Create state machine**.
