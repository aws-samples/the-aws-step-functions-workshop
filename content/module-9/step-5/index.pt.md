---
title: 'Limpeza'
weight: 115
---

:::alert{header="Importante" type="warning"}
Siga as instruções nesta página se desejar limpar recursos em sua própria conta. As contas do Event Engine não requerem limpeza.
:::

## Exclua manualmente a máquina de estado

Navegue até **Step Functions**. 
Se você nomeou a máquina de estado de acordo com as instruções fornecidas:

- Selecione **DetectSentimentMachine** da lista de máquinas de estado.
- Clique no botão **Delete**
- Confirme clicando no botão **Delete state machine** na caixa de diálogo exibida.

- Navegue até a página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) no Console da AWS.
- Selecione a pilha com o nome `SFW-Module-9` (ou qualquer nome que você tenha escolhido para a pilha) e clique em Excluir.
  ![CloudFormation exclusão](/static/img/setup/setup-cloudformation-delete.png)
- Certifique-se de que a exclusão da pilha seja concluída com êxito.
