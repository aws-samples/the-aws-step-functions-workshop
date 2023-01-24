---
title: 'Ejecutar la máquina de estados'
weight: 113
---

- Haz clic en **Start execution** y utiliza lo siguiente como entrada.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "Estoy muy feliz de aprender sobre Step Functions!"
}
:::

- Inspecciona **Execution event history** para ver una lista de eventos y encontrar uno llamado **TaskSucceeded**. Haz clic para expandir este evento y deberías encontrar el sentimiento detectado para su comentario.
- Siéntete libre de ejecutar la máquina de estados de nuevo con otras entradas en el campo Comment y ver los resultados del análisis de sentimiento de Comprehend. 

::alert[**¡Enhorabuena!** Has completado con éxito una integración de servicio AWS SDK.]{type="success"}

