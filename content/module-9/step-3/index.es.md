---
title: 'Crear la máquina de estado y provisionar recursos'
weight: 112
---

1. Navega a [Step Functions](https://console.aws.amazon.com/states/home) en su consola de AWS. Asegúrese de estar en la región correcta.

2. Si no está en la página `State machines`, Haz clic en `State machines` en el menú de la izquierda y Haz clic en **Create state machine**

3. Para `Choose authoring method` selecciona **Design your workflow visually**, selecciona el tipo de máquina de estado `Type` como **Standard** y Haz clic en `Next`.
   ![Studio](/static/img/module-6/studio-selection.png)

4. Deberías ver el estudio del diseñador ahora, que se verá así.
   ![](/static/img/module-6/studio-designer.png)

5. Ingresa un `Comentario` en el lado derecho: 

```bash
Un flujo de trabajo que contiene una integración del servicio AWS SDK con Amazon Comprehend.
```

6. En el menú **Actions** del lado izquierdo, utiliza la barra de búsqueda y busca `DetectSentiment`. Deberías ver la acción **Comprehend DetectSentiment**.

7. Arrastra y suelta `DetectSentiment` desde la sección **Actions** del lado izquierdo, hacia donde dice `Drag first state here` en el lado derecho.
   ![](/static/img/module-9/detect-sentiment.png)
   ![](/static/img/module-9/detect-sentiment-state.png)

8. Haz clic en la acción de Comprehend.
9. Actualiza los parámetros de la API en la sección **Configuration** para utilizar lo siguiente:
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "LanguageCode": "en",
  "Text.$": "$.Comment"
}
:::

La máquina de estado pasará el valor Comment de la entrada de ejecución a Comprehend para el análisis de sentimiento.

10. Utiliza los valores predeterminados para **Input, Output and Error handling**. Haz clic en el botón **Definition** para revisar la sintaxis ASL que generará.
    
11. Ahora Haz clic en **Next** y revisa el código generado. Haz clic en **Next** de nuevo.
12. Proporcione un nombre a su máquina de estado, `DetectSentimentMachine`.

13. Haz clic en el botón **Choose existing role*** y selecciona `UniversalSDKRoleNameforStepfunctions` desde el menú desplegable.

![](/static/img/module-9/iam.png)

14. Ahora Haz clic en **Create state machine**.

15. Has creado con éxito la máquina de estado.
