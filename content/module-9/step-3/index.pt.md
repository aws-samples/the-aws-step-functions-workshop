---
title: 'Criar a máquina de estado e provisionar recursos'
weight: 112
---

1. Navegue até  [Step Functions](https://console.aws.amazon.com/states/home) em seu console da AWS. Verifique se você está na região correta.

2. Se você não estiver na página `State machines`, clique em `State machines` no menu do lado esquerdo e clique em **Create state machine**

3. Em `Choose authoring method` selecione **Design your workflow visually**, e selecione `Type` as **Standard** e clique em `Next`.
   ![Studio](/static/img/module-6/studio-selection.png)

4. Você deve ver agora o designer studio que será como na imagem abaixo:
   ![](/static/img/module-6/studio-designer.png)

5. Insira um comentário no lado direito no campo `Comment - optional`: 

```bash
Um fluxo de trabalho que contém uma integração de serviço do AWS SDK com o Amazon Comprehend.
```

6. No menu **Actions** do lado esquerdo, use a barra de pesquisa e pesquise por `DetectSentiment`. Você deve ver a ação **Comprehend DetectSentiment** aparecer.

7. Arraste e solte `DetectSentiment` da seção **Actions** no lado esquerdo para o formulário do designer, onde está escrito `Drag first state here`.
   ![](/static/img/module-9/detect-sentiment.png)
   ![](/static/img/module-9/detect-sentiment-state.png)

8. Clique na ação do Comprehend `DetectSentiment`.
9. Atualize os API Parameters na seção **Configuration** para usar o seguinte:
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "LanguageCode": "en",
  "Text.$": "$.Comment"
}
:::

A máquina de estado passará o valor do comentário da entrada de execução para o Comprehend para análise de sentimentos.

10. Use as configurações padrões para **Input, Output e Error handling**. Clique no botão **Definition** para revisar a sintaxe ASL que você gerará.
    
11. Agora clique em **Next** e revise o código gerado. Clique em **Next** novamente.
12. Forneça um nome para sua máquina de estado, `DetectSentimentMachine`.

13. Clique em **Choose existing role** e selecione `UniversalSDKRoleNameforStepfunctions` do menu suspenso.

![](/static/img/module-9/iam.png)

14. Agora clique em **Create state machine**.

15. Você criou a máquina de estado com sucesso.
