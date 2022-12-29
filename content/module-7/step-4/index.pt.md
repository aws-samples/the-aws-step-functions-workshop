---
title: 'Construa uma máquina de estado com um Parallel State e integre-a com o API Gateway'
weight: 94
---

### Criar a Máquina de Estado

Siga os passos abaixo para criar uma máquina de estado usando o Workflow Studio.

1. Navegue até [Step Functions](https://console.aws.amazon.com/states/home) no console da AWS. Certifique-se de que você está na região certa.
2. Clique em **Create state machine**.
3. Em `Choose authoring method`, selecione **Design your workflow visually**, então selecione o tipo da máquina de estado em `Type` como **Express** e clique em `Next`.
   ![Studio Selection](/static/img/module-7/studio-selection.png)
4. Você deve ver a página do Workflow Studio.
   ![Studio Designer](/static/img/module-7/studio-designer.png)
5. Digite o seguinte comentário em `Comment` no lado direito da tela: 

```bash
Um fluxo de trabalho que executa tarefas em paralelo.
```

6. Arraste e solte `Parallel` da seção **Flow** do lado esquerdo da tela para o designer onde diz `Drag first state here`.
   ![Add Parallel State](/static/img/module-7/add-parallel-state.png)
7. Você deve ter as três funções Lambda para esse módulo criadas na sua conta. Adicione uma ação para invocar a primeira função Lambda.

- Arraste e solte `AWS Lambda Invoke` da seção **Actions** ao lado esquerdo da tela para o designer onde diz `Drag state here`.
  ![Invoke Lambda Function 1](/static/img/module-7/lambda-invoke-function1.png)
- Na aba `Configuration` do designer, digite `SumValues` para o **State name**. 
- Na seção de API parameters, selecione do drop down de **Function name** a função com `SumFunction` no nome.
  ![Configuration Sum State](/static/img/module-7/configuration-sum-state.png)
- Na aba `Output`, desmarque a opção `Filter output with OutputPath` e marque a opção `Transform result with ResultSelector`. Cole o seguinte texto em JSON no campo de texto:

  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "sum.$": "$.Payload.sum" }
  :::
  ![Output Sum State](/static/img/module-7/output-sum-state.png)

8. Adicione uma ação para invocar a segunda função Lambda.

- Arraste e solte `AWS Lambda Invoke` da seção **Actions** ao lado esquerdo da tela para o designer onde diz `Drag state here`.
  ![Invoke Lambda Function 2](/static/img/module-7/lambda-invoke-function2.png)
- Na aba `Configuration` do designer, digite `AverageValues` para o **State name**.
- Na seção API parameters, selecione do drop down **Function name** a função com `AvgFunction` no nome.
  ![Configuration Avg State](/static/img/module-7/configuration-avg-state.png)
- Na aba `Output`, desmarque a opção `Filter output with OutputPath` e marque a opção `Transform result with ResultSelector`, depois cole o seguinte texto em JSON no campo de texto:
  :::code{showCopyAction=true showLineNumbers=true language=json}
  { "avg.$": "$.Payload.avg" }
  :::
  ![Output Avg State](/static/img/module-7/output-avg-state.png)

9. Adicione uma ação para invocar a terceira função Lambda.

- Arraste e solte `AWS Lambda Invoke` da seção **Actions** ao lado esquerdo da tela para o designer entre as duas ações existentes.
  ![Invoke Lambda Function 3](/static/img/module-7/lambda-invoke-function3.png)
- Na aba `Configuration` do designer, digite `MaxMinValues` para o **State name**.
- Na seção API parameters, selecione do drop down **Function name** a função com `MaxMinFunction` no nome.
  ![Max Min State](/static/img/module-7/configuration-maxmin-state.png)
- Na aba `Output`, desmarque a opção `Filter output with OutputPath` e marque a opção `Transform result with ResultSelector`, depois cole o seguinte texto em JSON no campo de texto:
:::code{showCopyAction=true language=json}
{
"max.$": "$.Payload.max",
"min.$": "$.Payload.min"
}
:::
  ![Output Max Min State](/static/img/module-7/output-maxmin-state.png)

10. Clique em **Next** e revise o código gerado, então clique **Next** de novo.

- Digite um nome para essa máquina de estado: `ParallelProcessingMachine`. Escolha uma role IAM existente que contém `StepFunctionsIamRole` no nome.
- Deixe o restante dos valores padrões e clique em **Create state machine**.
  Agora você tem uma máquina de estado que pode rodar cálculos paralelos. Copie a ARN da Máquina de Estado e salve. Você vai precisar dessa informação para criar a integração com o API Gateway.

### Como configurar a integração entre o API Gateway e o Step Functions

1. Navegue para o [console do API Gateway](https://console.aws.amazon.com/apigateway/home) e selecione a API criada para esse módulo: `API Gateway State Machine integration`.
   ![API Console](/static/img/module-7/api-console.png)
2. Da lista de recursos, ache o recurso `execution` e clique em `POST`.
   ![API Execution](/static/img/module-7/pt-br/api-execution.png)
3. Clique em `Solicitação de Integração`
4. Para o `Tipo de Integração` selecione `Serviço da AWS`
5. Configure a integração:

- **Região da AWS**: selecione a região da AWS onde você criou a Máquina de Estado
- **Serviço da AWS**: selecione `Step Functions` do drop down
- **Método HTTP**: selecione `POST`
- **Tipo de ação**: selecione `Usar nome da ação`
- **Ação**: `StartExecution`
- **Função de execução**: ache no [IAM](https://console.aws.amazon.com/iamv2/home) a role com `IntegrationIamRole` no nome e use a ARN dessa role
  ![API Integration Setup](/static/img/module-7/pt-br/api-integration-setup.png)
- Clique `Save`. Quando solicitado, se você tiver certeza que quer alterar a integração, clique em `Ok`.
  Você acaba de configurar a integração entre o API Gateway e o Step Functions.
