---
title: 'Módule 5 - Estado Choice e Estado Map'
weight: 70
---

## Estado Choice
Um [estado Choice](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-choice-state.html) adiciona lógica condicional a uma máquina de estado. Além da maioria dos campos dos campos comuns, o estado `Choice` possui os campos adicionais abaixo:

- Choices (Obrigatório) - um conjunto de regras de escolha que determinar qual será o próximo estado da máquina de estados.

- Default (Opcional, Recomendado) - o nome de um estado para o qual a máquina de estados deve mudar caso nenhuma regra do campo Choice seja atendida.

## Estado Map 
Se uma carga de trabalho possui uma quantidade desconhecida de ramificações, o [estado Map](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html) pode executar um conjunto de etapas em paralelo para cada item de uma matriz de entrada. Para configurar o estado `Map` defina um `Iterator`, que é um sub fluxo de trabalho. Quando a execução do Step Functions entrar no estado `Map`, ele irá executar as mesmas etapas para cada entrada existente na matriz de entrada do estado. Para cada item o estado `Map` executará um sub fluxo de trabalho, preferencialmente em paralelo. Quando todos os sub fluxos de trabalho terminarem, o estado `Map` retornará uma matriz contendo uma saída para cada item processado pelo Iterator.

**Duração estimada: 20 minutos**