---
title: 'Depure execuções com falha com o Rastreamento do AWS X-Ray'
weight: 145
---

Você pode usar o AWS X-Ray para visualizar as integrações em sua máquina de estado, identificar gargalos de desempenho e solucionar problemas de solicitações com falha. Quando sua máquina de estado envia dados de rastreamento para o X-Ray, o X-Ray processa os dados para gerar um mapa de serviço e resumos de rastreamento pesquisáveis.

Com o X-Ray habilitado para sua máquina de estado, você pode rastrear os caminhos de suas solicitações, fornecendo uma visão geral detalhada de todo o seu fluxo de trabalho. Você pode usar os mapas de serviço do X-Ray para visualizar a latência da solicitação, incluindo quaisquer serviços da AWS integrados ao X-Ray. Você também pode configurar e personalizar as regras de amostragem no X-Ray para controlar a frequência das solicitações registradas.

Para saber mais leia [AWS X-Ray and Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html).

## Ativar rastreamento de raios-X em DetectSentimentStateMachine.

1. Navegue para [Step Functions console](https://console.aws.amazon.com/states/home). Verifique se você está na região correta.

2. Clique em **DetectSentimentStateMachine** Máquina de estado.

3. Na página `DetectSentimentStateMachine`, clique em **Edit**.

4. Em `Tracing` na página Edit, selecione **Enable X-Ray tracing**.

:::alert{header="Important" type="warning"}
Para rastrear execuções com o X-Ray, a função de execução do Step Functions deve ter permissões do X-Ray. Você pode permitir que o Step Functions crie uma nova função para você com as permissões necessárias selecionando "Criar nova função" em Permissões ou adicioná-los manualmente à sua função existente. Isso já foi feito para você.
:::

5. Clique **Save** no topo da página.

6. Navegue para [X-Ray](https://console.aws.amazon.com/xray/home) no console AWS.

Aguarde alguns minutos até que o console do X-Ray seja carregado com o Service Map. Atualize a página, se necessário. Você verá o mapa de serviço a seguir para o DetectSentimentStateMachine.

   ![Service Map](/static/img/module-12/x-ray-service-map.png)

Este mapa de serviço mostra que sua máquina de estado interage com AWS Lambda e Amazon DynamoDB. A legenda vermelha no DetectSentimentStateMachine indica falhas. A legenda roxa no nó da tabela de sentimentos indica limitação.

7. Clique no nó **sentiment-table** para investigar essa limitação.

8. No painel de detalhes do serviço à direita, selecione **Throttle** e clique em **View Traces**

   ![View Traces](/static/img/module-12/x-ray-view-traces.png)

9. Na página `Traces` na lista Trace, clique em um dos traces.

   ![View Traces](/static/img/module-12/x-ray-traces-list.png)

10. Na página Trace details, você verá um ícone de erro no segmento AWS::StepFunctions::StateMachine.

    ![View Traces](/static/img/module-12/x-ray-trace-error.png)

11. Mais abaixo no Trace, há um erro próximo ao subsegmento Record Transition. Clique no ícone de erro.

    ![View Traces](/static/img/module-12/x-ray-exception.png)

O erro é causado pela limitação da taxa de transferência provisionada do DynamoDB. A taxa de transferência solicitada excedeu o nível configurado de capacidade provisionada. Para resolver o problema, você pode reduzir a taxa de transferência solicitada diminuindo a frequência de suas gravações ou pode aumentar sua capacidade aumentando suas unidades de capacidade de gravação provisionadas ou alterando o modo de cobrança do DynamoDB de provisionado para sob demanda.








