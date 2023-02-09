---
title: 'Usar Workflow Studio para construir una máquina de estados'
weight: 83
---

1. Navega a [Step Functions](https://console.aws.amazon.com/states/home) en su consola de AWS. Asegúrate de estar en la región de AWS correcta.

2. Haz clic en el botón **Create state machine**.

3. Para `Choose authoring method` selecciona **Design your workflow visually**, selecciona el tipo de máquina de estado `Type` como **Standard** y haz clic en **Next**.
   ![Studio](/static/img/module-6/studio-selection.png)

4. Deberías ver el Workflow Studio ahora.
   ![Studio Designer](/static/img/module-6/studio-designer.png)

5. Ingresa un comentario en el campo `Comment` en el lado derecho:

```bash
Un ejemplo de funciones de paso que muestra el procesamiento de entrada y salida.
```

6. Arrastra la acción **AWS Lambda Invoke** de la sección `Actions` en el lado izquierdo, y suéltala en el formulario del diseñador donde dice `Drag first state here`.
   ![Lambda Invoke](/static/img/module-6/lambda-invoke-state.png)

7. Configura el estado.

- En la pestaña `Configuration` del diseñador, ingresa un nombre para este estado: `Invoke HelloFunction`.
- Deberías tener una función Lambda llamada `HelloFunction` ya implementada en su cuenta.
- Configura este estado para invocar esa función. Encuentra el campo `API Parameters` y haz clic en `Function name`. Desplázate por la lista de menú hasta encontrar **HelloFunction:$LATEST**. Selecciona este valor.

![Configuration](/static/img/module-6/configuration.png)

- Haz clic en la pestaña `Input` y marca la casilla para `Filter input with InputPath - optional`. Ingresa `$.lambda` para el valor.
  ![Config Input](/static/img/module-6/config-input.png)
- Haz clic en la pestaña `Output` y marca la casilla para `Add original input to output using ResultPath - optional`. Selecciona `Combine original input with result`. Ingresa la siguiente cadena como el filtro ResultPath: `$.data.lambdaresult`.
- Marca la casilla para `Filter output with OutputPath` e ingresa `$.data` para el valor.
  ![Config Output](/static/img/module-6/config-output.png)
- Haz clic en la pestaña `Error handling`. Encuentra la sección **Retry on errors** y elimina el `Retrier #1` predeterminado haciendo clic en el icono de edición a la derecha y desplazándote hacia abajo para hacer clic en el botón **Remove**.
  ![Remove Retrier](/static/img/module-6/remove-retrier.png)
- Haz clic en **Next** y revisa el código generado y haz clic en **Next** nuevamente.
- Ingresa el nombre de la máquina de estados: `InputOutputProcessingMachine`. Para el rol de ejecución, elige un rol existente: `InputOutputProcessingStepFunctionRole`
  ![Iam Role](/static/img/module-6/name-iam-role.png)
- Deja los valores predeterminados restantes y haz clic en **Create state machine**.
