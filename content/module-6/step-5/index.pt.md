---
title: 'Use o Simulador de Fluxo de Dados para testar processamento de dados'
weight: 85
---

## Usando o Simulador de Fluxo de Dados (Data Flow Simulator)

1. Clique no botão **Data flow simulator** no Graph Inspector.

O Simulador de Fluxo de Dados permite que os desenvolvedores simulem a ordem de processamento de dados que acontece em um estado durante sua execução. Isso ajuda os desenvolvedores a entenderem como filtrar e manipular dados conforme eles fluem de estado para estado. Os desenvolvedores podem especificar uma entrada JSON inicial e avaliá-la em cada um dos estágios do fluxo de processamento.

O simulador começa no estágio State Input. O campo de entrada de texto valida automaticamente o objeto JSON e destaca quaisquer erros de sintaxe.

![Data flow simulator](/static/img/module-6/simulator.png)

2. Use o Simulador de Fluxo de Dados para testar o processamento de dados para o payload de entrada `InputOutputProcessingMachine`. Substitua o valor padrão no State Input com o payload de entrada abaixo e depois selecione o estágio InputPath. Digite `$.lambda` no campo de texto do InputPath. 

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

![Data flow simulator](/static/img/module-6/input-path.png)

O painel à esquerda mostra o valor de entrada do estado antes de o InputPath ser aplicado. O painel à direita mostra o valor de entrada do estado após o InputPath ser aplicado. 

Desenvolvedores podem usar o Simulador de Fluxo de Dados para implementar rapidamente o processamento de dados que eles precisam em suas máquinas de estado. 
Sinta-se à vontade para continuar testando valores para ResultSelector e OutputPath no Simulador de Fluxo de Dados.

Para mais informações sobre o Simulador de Fluxo de Dados, acesse o [AWS Blog](https://aws.amazon.com/blogs/compute/modeling-workflow-input-output-path-processing-with-data-flow-simulator/).
 
::alert[**Parabéns!** Você usou o Simulador de Fluxo de Dados para praticar processamento de dados de Entrada e Saída usando o Amazon States Language (ASL)!]{type="success"}
