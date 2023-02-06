---
title: 'Use o Workflow Studio para construir uma máquina de estado'
weight: 83
---

1. Navegue até [Step Functions](https://console.aws.amazon.com/states/home) no seu console da AWS. Tenha certeza que você está na região da AWS certa.

2. Clique em **Create state machine**.

3. Em `Choose authoring method` selecione **Design your workflow visually**, selecione **Standard** em `Type` para definir o tipo de máquina de estado e clique em **Next**.
   ![Studio](/static/img/module-6/studio-selection.png)

4. A página de Workflow Studio deve aparecer.
   ![Studio Designer](/static/img/module-6/studio-designer.png)

5. Escreva um comentário no campo `Comment` no lado direito da tela: 

```bash
Um exemplo de Step Function mostrando input e output.
```

6. Arraste e solte a ação **AWS Lambda Invoke** da seção **Actions** no lado esquerdo da tela, para onde diz `Drag first state here`.
   ![Lambda Invoke](/static/img/module-6/lambda-invoke-state.png)

7. Configure o estado: 

- Na aba **Configuration** do designer, em **State name**, escreva o nome para esse estado: `Execute HelloFunction`.
- Você deve ter uma função Lambda chamada `HelloFunction` já provisionada na sua conta.
- Configure esse estado para invocar a função Lambda. Ache o campo `API Parameters` e clique em `Enter function name`. Desça no menu até achar **HelloFunction:$LATEST**. Selecione esse valor. 

![Configuration](/static/img/module-6/configuration.png)

- Clique na aba `Input` e clique na caixa de seleção `filter input with InputPath - optional`. Digite `$.lambda` no campo de texto. 
  ![Config Input](/static/img/module-6/config-input.png)
- Clique na aba `Output` e clique na caixa de seleção `Add original input to output using ResultPath`. Selecione `Combine original input with result`. Digite o seguinte texto como o filtro ResultPath: `$.data.lambdaresult`.
- Clique na caixa de seleção `Filter output with OutputPath` e digite `$.data` no campo de texto.
  ![Config Output](/static/img/module-6/config-output.png)
- Clique na aba `Error handling`. Ache a seção **Retry on errors** e remova o valor padrão `Retrier #1` clicando no ícone de editar à direita e rolando a tela para baixo para clicar no botão **Remove**. 
  ![Remove Retrier](/static/img/module-6/remove-retrier.png)
- Clique em **Next** e revise o código gerado. Depois clique em **Next** novamente.
- Digite um nome para a State Machine (Máquina de Estado): `InputOutputProcessingMachine`. Em Execution role, selecione `choose an existing role` e escolha: `InputOutputProcessingStepFunctionRole`
  ![Iam Role](/static/img/module-6/name-iam-role.png)
- Deixe o restante dos valores padrões e clique em **Create state machine**.
