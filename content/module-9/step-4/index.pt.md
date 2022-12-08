---
title: 'Execute a máquina de estado'
weight: 113
---

- Clique em **Start execution** e use o seguinte como input, e clique novamente em `Start execution`.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "I am very happy to learn about Step Functions!"
}
:::

- Inspecione o **Execution event history** para ver uma lista de eventos e encontrar um chamado **TaskSucceeded**. Clique para expandir esse evento e você deverá encontrar o sentimento detectado em seu comentário.
- Sinta-se à vontade para executar a máquina de estado novamente com outras entradas no campo Comentário e ver os resultados da análise de sentimentos do Comprehend. 

::alert[**Parabéns!** Você concluiu com êxito a integração de serviço do AWS SDK.]{type="success"}
