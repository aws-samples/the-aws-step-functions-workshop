---
title: 'Ejecutar la máquina de estados'
weight: 113
---

- Haga clic en **Start execution** y utilice lo siguiente como entrada.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "Estoy muy feliz de aprender sobre Step Functions!"
}
:::

- Inspeccione **Execution event history** para ver una lista de eventos y encontrar uno llamado **TaskSucceeded**. Haga clic para expandir este evento y debería encontrar el sentimiento detectado para su comentario.
- Siéntase libre de ejecutar la máquina de estados de nuevo con otras entradas en el campo Comment y ver los resultados del análisis de sentimiento de Comprehend. 

::alert[**¡Enhorabuena!** Ha completado con éxito una integración de servicio AWS SDK.]{type="success"}

