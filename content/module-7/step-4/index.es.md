---
title: 'Construir una máquina de estado con un Estado Paralelo e Integrarlo con API Gateway'
weight: 94
---

### Crear la máquina de estado

Siga los siguientes pasos para crear una máquina de estado utilizando Workflow Studio.

1. Navegue a [Step Functions](https://console.aws.amazon.com/states/home) en su consola de AWS. Asegúrese de estar en la región correcta.
2. Haga clic en **Create state machine**.
3. Para `Choose authoring method` seleccione **Design your workflow visually**, seleccione el tipo de máquina de estado `Type` como **Express** y haga clic en `Next`.
   ![Studio Selection](/static/img/module-7/studio-selection.png)
4. Debería ver Workflow Studio.
   ![Studio Designer](/static/img/module-7/studio-designer.png)
5. Ingrese un `Comentario` en el lado derecho: 

```bash
Un flujo de trabajo de funciones step que ejecuta tareas en paralelo.
```

6. Arrastra y suelta `Parallel` desde la sección **Flow** en el lado izquierdo en el formulario del diseñador donde dice `Drag first state here`.
   ![Add Parallel State](/static/img/module-7/add-parallel-state.png)
7. Deberías tener las tres funciones Lambda para este módulo desplegadas en tu cuenta. Agrega una acción para invocar la primera función Lambda.

- Arrastra y suelta `AWS Lambda Invoke` desde la sección **Accions** en el lado izquierdo en el formulario del diseñador donde dice `Drag state here`.
  ![Invoke Lambda Function 1](/static/img/module-7/lambda-invoke-function1.png)
- En la pestaña `Configurationn` del diseñador, ingresa `SumValues` para el nombre del estado.
- En la sección de parámetros de la API, selecciona desde el menú desplegable de **Function name** la función con `SumFunction` en el nombre.
  ![Configuraction Sum State](/static/img/module-7/configuration-sum-state.png)
- En la pestaña `Output`, desmarca la opción para `Filter output with OutputPath` y marca la opción para `Transform result with ResultSelector`. Pega el siguiente json en el cuadro de texto:

  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "sum.$": "$.Payload.sum" }
  :::
  ![Output Sum State](/static/img/module-7/output-sum-state.png)

8. Agrega una acción para invocar la segunda función Lambda.

- Arrastra y suelta `AWS Lambda Invoke` desde la sección **Actions** en el lado izquierdo en el formulario del diseñador donde dice `Drag state here`.
  ![Invoke Lambda Function 2](/static/img/module-7/lambda-invoke-function2.png)
- En la pestaña `Configuration` del diseñador, ingresa `AverageValues` para el nombre del estado.
- En la sección de parámetros de la API, selecciona desde el menú desplegable de **Function name** la función con `AvgFunction` en el nombre.
  ![Configurationn Avg State](/static/img/module-7/configuration-avg-state.png)
- En la pestaña `Output`, desmarca la opción para `Filter output with OutputPath` y marca la opción `Transform result with ResultSelector`, entonce pega el siguiente json en el cuadro de texto
  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "avg.$": "$.Payload.avg" }
  :::
  ![Output Avg State](/static/img/module-7/output-avg-state.png)

9. Agregar una acción para invocar la tercera función Lambda.

- Arrastre y suelte `AWS Lambda Invoke` desde la sección **Actions** en el lado izquierdo en el formulario del diseñador entre las dos acciones existentes.
  ![Invoke Lambda Function 3](/static/img/module-7/lambda-invoke-function3.png)
- En la pestaña `Configuration` del diseñador, ingrese `MaxMinValues` para el nombre del estado.
- En la sección de parámetros de la API, seleccione desde el menú desplegable de **Function name** el que tenga `MaxMinFunction` en su nombre.
  ![Max Min State](/static/img/module-7/configuration-maxmin-state.png)
- En la pestaña `Output`, desmarque la opción de `Filter output with OutputPath` y marque la opción de `Transform result with ResultSelector` y pegue el siguiente json en el cuadro de texto
:::code{showCopyAction=true language=json}
{
"max.$": "$.Payload.max",
"min.$": "$.Payload.min"
}
:::
![Output Max Min State](/static/img/module-7/output-maxmin-state.png)

10. Haga clic en **Next** y revise el código generado y haga clic en **Next** de nuevo.

- Proporcione un nombre a esta máquina de estado: `ParallelProcessingMachine`. Elija un rol de IAM existente con el nombre que contenga `StepFunctionsIamRole`.
- Deje el resto de las opciones predeterminadas y haga clic en **Create state machine**.
  Ahora tiene una máquina de estado que puede ejecutar cálculos en paralelo. Copie el ARN de la máquina de estado y guárdelo. Lo necesitará para crear la integración con API Gateway.

### Configuración de la integración entre API Gateway y Step Functions

1. Vaya a la [consola de API Gateway](https://console.aws.amazon.com/apigateway/home) y seleccione la API creada para este módulo: `API Gateway State Machine integration`.
   ![API Console](/static/img/module-7/api-console.png)
2. Entre la lista de recursos, encuentre el recurso de ejecución y haga clic en `POST`
   ![API Execution](/static/img/module-7/api-execution.png)
3. Haga clic en `Solicitud de integración`
4. Para el tipo de integración seleccione `Servicio de AWS`
5. Configure la integración:

- **Región de AWS**: seleccione la región de AWS donde creó la máquina de estado
- **Servicio de AWS**: seleccione `Step Functions` desde el menú desplegable
- **Método HTTP**: seleccione `POST`
- **Tipo de acción**: seleccione `Usar nombre de acción`
- **Action**: escriba `StartExecution`
- **Role de ejecución**: encuentre en [IAM](https://console.aws.amazon.com/iamv2/home) el rol con `IntegrationIamRole` en su nombre y utilice el ARN de este rol
  ![API Integration Setup](/static/img/module-7/api-integration-setup.png)
- Haga clic en `Guardar`. Cuando se le solicite si está seguro de que desea cambiar la integración, haga clic en `Aceptar`.
  Ahora ha configurado una integración entre la API Gateway y las funciones Step.
