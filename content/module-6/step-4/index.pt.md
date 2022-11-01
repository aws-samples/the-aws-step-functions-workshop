---
title: 'Execute a máquina de estado e revise os resultados'
weight: 84
---

1. Clique na máquina de estado `InputOutputProcessingMachine` no console do Step Functions.
2. Clique em **Start execution** e use o texto em JSON abaixo como `input payload`:
:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "An input comment.",
   "data": {
      "value1": 23,
      "value2": 17
   },
   "extra": "foo",
   "lambda": {
      "who": "AWS Step Functions"
   }
}
:::
3. Quando a execução finalizar, revise o resultado na aba `Execution output`. Observe como o texto em JSON do `input payload` é adicionado ao output da função Lambda. Esse output seria passado para o próximo estado do seu fluxo de trabalho. 

::alert[**Parabéns!** Você executou uma máquina de estado usando os recursos de processamento de Entrada e Saída.]{type="success"}