---
title: 'Construir una máquina de estado con un estado Parallel e integrarl con API Gateway'
weight: 94
---

### Crear la máquina de estado

Sigue los siguientes pasos para crear una máquina de estado utilizando Workflow Studio.

1. Navega a [Step Functions](https://console.aws.amazon.com/states/home) en tu consola de AWS. Asegúrate de estar en la región correcta.
2. Haz clic en **Create state machine**.
3. En el paso `Choose authoring method` selecciona **Design your workflow visually**, luego selecciona el tipo de máquina de estado `Type` como **Express** y haz clic en `Next`.
   ![Studio Selection](/static/img/module-7/studio-selection.png)
4. Deberías ver Workflow Studio.
   ![Studio Designer](/static/img/module-7/studio-designer.png)
5. Ingresa un `Comentario` en el lado derecho: 

```bash
Un flujo de trabajo de funciones step que ejecuta tareas en paralelo.
```

6. Desde la sección **Flow** en el lado izquierdo, arrastra y suelta `Parallel` en el formulario del diseñador donde dice `Drag first state here`.
   ![Add Parallel State](/static/img/module-7/add-parallel-state.png)
7. Deberías tener las tres funciones Lambda para este módulo desplegadas en tu cuenta. Agrega una acción para invocar la primera función Lambda.

- Desde la sección **Accions** en el lado izquierdo, arrastra y suelta `AWS Lambda Invoke` en el formulario del diseñador donde dice `Drag state here`.
  ![Invoke Lambda Function 1](/static/img/module-7/lambda-invoke-function1.png)
- En la pestaña `Configuration` del diseñador, ingresa `SumValues` para el nombre del estado.
- En la sección de parámetros de la API, selecciona desde el menú desplegable de **Function name** la función con `SumFunction` en el nombre.
  ![Configuraction Sum State](/static/img/module-7/configuration-sum-state.png)
- En la pestaña `Output`, desmarca la opción `Filter output with OutputPath` y marca la opción `Transform result with ResultSelector`, luego pega el siguiente json en el cuadro de texto:

  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "sum.$": "$.Payload.sum" }
  :::
  ![Output Sum State](/static/img/module-7/output-sum-state.png)

8. Agrega una acción para invocar la segunda función Lambda.

- Desde la sección **Actions** en el lado izquierdo, arrastra y suelta `AWS Lambda Invoke` en el formulario del diseñador donde dice `Drag state here`.
  ![Invoke Lambda Function 2](/static/img/module-7/lambda-invoke-function2.png)
- En la pestaña `Configuration` del diseñador, ingresa `AverageValues` para el nombre del estado.
- En la sección de parámetros de la API, selecciona desde el menú desplegable de **Function name** la función con `AvgFunction` en el nombre.
  ![Configurationn Avg State](/static/img/module-7/configuration-avg-state.png)
- En la pestaña `Output`, desmarca la opción `Filter output with OutputPath` y marca la opción `Transform result with ResultSelector`, luego pega el siguiente json en el cuadro de texto
  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "avg.$": "$.Payload.avg" }
  :::
  ![Output Avg State](/static/img/module-7/output-avg-state.png)

9. Agrega una acción para invocar la tercera función Lambda.

- Desde la sección **Actions** en el lado izquierdo, arrastra y suelta `AWS Lambda Invoke` en el formulario del diseñador entre las dos acciones existentes.
  ![Invoke Lambda Function 3](/static/img/module-7/lambda-invoke-function3.png)
- En la pestaña `Configuration` del diseñador, ingresa `MaxMinValues` para el nombre del estado.
- En la sección de parámetros de la API, selecciona desde el menú desplegable de **Function name** el que tenga `MaxMinFunction` en su nombre.
  ![Max Min State](/static/img/module-7/configuration-maxmin-state.png)
- En la pestaña `Output`, desmarca la opción `Filter output with OutputPath` y marca la opción `Transform result with ResultSelector`, luego pega el siguiente json en el cuadro de texto
:::code{showCopyAction=true language=json}
{
"max.$": "$.Payload.max",
"min.$": "$.Payload.min"
}
:::
![Output Max Min State](/static/img/module-7/output-maxmin-state.png)

10. Haz clic en **Next**, revisa el código generado y haz clic en **Next** de nuevo.

- Proporciona un nombre a esta máquina de estado: `ParallelProcessingMachine`. Elige un rol de IAM existente con el nombre que contenga `StepFunctionsIamRole`.
- Deja el resto de las opciones predeterminadas y haz clic en **Create state machine**.
  Ahora tienes una máquina de estado que puede ejecutar cálculos en paralelo. Copia el ARN de la máquina de estado y guárdalo, lo necesitarás luego para crear la integración con API Gateway.

### Configuración de la integración entre API Gateway y Step Functions

1. Ve a la [consola de API Gateway](https://console.aws.amazon.com/apigateway/home) y selecciona la API creada para este módulo: `API Gateway State Machine integration`.
   ![API Console](/static/img/module-7/api-console.png)
2. Entra a la lista de recursos, encuentra el recurso de `/execution` y haz clic en `POST`
   ![API Execution](/static/img/module-7/api-execution.png)
3. Haz clic en `Solicitud de integración`
4. Para el tipo de integración selecciona `Servicio de AWS`
5. Configura la integración:

- **Región de AWS**: selecciona la región de AWS donde se creó la máquina de estado
- **Servicio de AWS**: selecciona `Step Functions` desde el menú desplegable
- **Método HTTP**: selecciona `POST`
- **Tipo de acción**: selecciona `Usar nombre de acción`
- **Action**: escribe `StartExecution`
- **Role de ejecución**: busca en [IAM](https://console.aws.amazon.com/iamv2/home) el rol con `IntegrationIamRole` en su nombre y utiliza el ARN de este rol
  ![API Integration Setup](/static/img/module-7/api-integration-setup.png)
- Haz clic en `Guardar`. Cuando se te solicite si estás seguro que deseas cambiar la integración, haz clic en `Aceptar`.
  Ahora has configurado una integración entre API Gateway y Step Functions.
