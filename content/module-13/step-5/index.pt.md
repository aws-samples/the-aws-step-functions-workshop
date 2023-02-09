---
title: 'Revise o impacto dos custos'
weight: 155

---

Optmização de custos é um motivo chave para se adotar fluxos de trabalhos Express aninhados em fluxos de trabalhos Standards.  

## Precificação

|**Standard Workflows**|**Express Workflows**|
---|---|
|Standard Workflows são cobrados baseados nas transições de estados necessárias para o fluxo de trabalho. Step Functions conta uma transição de estado sempre que uma etapa do seu fluxo de trabalho é executado. Você é cobrado pelo numero total de transições de estados em todo a sua máquina de estados Standard, incluindo retries.|Express Workflows são cobrados baseados no número de vezes que sua máquina de estados executou e na duração. Duração começa a ser calculada quando seu fluxo de trabalho começa a executação até ele completar ou ser finalizado de outra maneira, contando de 100ms em 100ms, e a quantidade de memória utilizada para executar o fluxo de trabalho, cobrado de 64-MB em 64-MB.|

## Comparação de custos

Substituindo as quatro etapas que executam Lambda em nosso fluxo de trabalho Standard pelas etapas de execução dentro do fluxo de trabalho Express aninhado, eliminamos 3 etapas em cada execução de nossa máquina de estados Standard.

Vamos dizer que você executou o fluxo de trabalho Standard 1,000 vezes na região de N. Virginia. Você seria cobrado por 3.000 transições de estado a mais do que usando o fluxo de trabalho modificado.

### Fluxo de trabalho Original

**Custo total** = `(número de transições por execução x número de execuções) x $0.000025`  
**Custo total** = `(3 X 1000) X 0.000025 = $0.075`  
(*Note: Isso não inclui as 4.000 transições de estados existentes no AWS Free Tier mensal*)  

### Fluxos de trabalho Express aninhados

Ao invés, você agora é cobrado pelo fluxo de trabalho Express. Vamos assumir que cada execução do fluxo de trabalho Express demore uma média de 11.300ms e não use mais que 64-MB de memória.  

**Custo de duração** = `(Duração média cobrada ms / 100) * preço por 100 ms`  
**Custo de execução** = `$0.000001 por solicitação`  
**Custo total** = `(Custo de execução + Custo de duração) x Número de solicitações`  

**Custo de duração** = `(11300 MS /100) * $ 0.0000001042 = $0.0000117746`  
**Custo de execucão** = `$0.000001 por solicitação`  
**Custo total** = `($0.000001 + $0.0000117746) x 1000 = $0.01`  

Resumindo, neste exemplo, custa 7.5x mais manter aquelas etapas no fluxo de trabalho Standard. Substituindo as etapas que não requerem garantia de execução do fluxo de trabalho Standard pelo fluxo de trabalho Express aninhado pode resultar em economia para sua carga de trabalho.

## Como a duração do fluxo de trabalho Express afeta o custo

A economina de custo dependerá do número de etapas que você removerá do fulxo de trabalho Standard e do tempo de execução. Se as etapas demoram muito tempo (mas ainda é executado em menos de 5 minutos que é o limte do fluxo de trabalho Express), pode ser menos custoso deixá-lo no fluxo de trabalho Standard. No exemplo, você removeu 3 transições de estado substituindo 4 tarefas por um fluxo de trabalho Express. O gráfico abaixo mostra o custo de 1.000 execuções de 3 etapas de um fluxo de trabalho Standard, plotado contra as mesmas 3 etapas executads no fluxo de trabalho Express aninhado com diferentes durações. Você consegue ver o range de durações onde o fluxo de trabalho Express é mais barato. para ver mais informações sobre o custo de execução dos fluxos de trabalho Standard e Express, veja a [Calculadora de preços AWS](https://calculator.aws/).

![Gráfico de comparação de custos](/static/img/module-13/cost-comparison-by-duration.png)

## Conclusão

Neste módulo, nós conseguimos reduzir o custo movendo etapas do fluxo de trabalho Standard para um fluxo de trabalho Express aninhado. Como mencionado [na introdução](../), você pode se beneficiar tanto da redução de custos como da modularização. Abaixo você encontra outros exemplos onde pode-se usar um fluxo de trabalho Express aninhado a um fluxo de trabalho Standard:

1. Uma máquina de estados que retorna dados de várias origens e executa algumas etapas de pré-processamento.
2. Um estado [Map inline](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-asl-use-map-state-inline.html) que executa várias etapas para centenas ou milhares de items.
3. Um sub-processo mantido por um time que é usado por outros times. Por exemplo, enviar uma notificação para usuários pode exigir obter seu meio de contato preferido em um sistema de CRM, checar se ele autoriza receber determinados tipos de mensagens, checar por promoções disponíveis, etc.