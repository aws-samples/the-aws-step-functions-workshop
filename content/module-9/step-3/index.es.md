---
title: 'Crear la máquina de estado y provisionar recursos'
weight: 112
---

1. Navegue a [Step Functions](https://console.aws.amazon.com/states/home) en su consola de AWS. Asegúrese de estar en la región correcta.

2. Si no está en la página `State machines`, haga clic en `State machines` en el menú de la izquierda y haga clic en **Create state machine**

3. Para `Choose authoring method` seleccione **Design your workflow visually**, seleccione el tipo de máquina de estado `Type` como **Standard** y haga clic en `Next`.
   ![Studio](/static/img/module-6/studio-selection.png)

4. Debería ver el estudio del diseñador ahora, que se verá así.
   ![](/static/img/module-6/studio-designer.png)

5. Ingrese un `Comment` en el lado derecho: 

```bash
Un flujo de trabajo que contiene una integración del servicio AWS SDK con Amazon Comprehend.
```

6. En el menú **Actions** del lado izquierdo, utilice la barra de búsqueda y busque `DetectSentiment`. Debería ver la acción **Comprehend DetectSentiment**.

7. Arrastre y suelte `DetectSentiment` desde la sección **Actions** del lado izquierdo, hacia donde dice `Drag first state here` en el lado derecho.
   ![](/static/img/module-9/detect-sentiment.png)
   ![](/static/img/module-9/detect-sentiment-state.png)

8. Haga clic en la acción de Comprehend.
9. Actualice los parámetros de la API en la sección **Configuration** para utilizar lo siguiente:
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "LanguageCode": "en",
  "Text.$": "$.Comment"
}
:::

La máquina de estado pasará el valor Comment de la entrada de ejecución a Comprehend para el análisis de sentimiento.

10. Utilice los valores predeterminados para **Input, Output and Error handling**. Haga clic en el botón **Definition** para revisar la sintaxis ASL que generará.
    
11. Ahora haga clic en **Next** y revise el código generado. Haga clic en **Next** de nuevo.
12. Proporcione un nombre a su máquina de estado, `DetectSentimentMachine`.

13. Haga clic en el botón **Choose existing role*** y seleccione `UniversalSDKRoleNameforStepfunctions` desde el menú desplegable.

![](/static/img/module-9/iam.png)

14. Ahora haga clic en **Create state machine**.

15. Ha creado con éxito la máquina de estado.
