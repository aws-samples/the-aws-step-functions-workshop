---
title: 'Limpar os recursos'
weight: 86
---
:::alert{header="Importante" type="warning"}
Siga as instruções nessa página se você gostaria de limpar os recursos da sua própria conta AWS. Para contas do Event Engine não é necessário executar esses passos. 
:::

## Excluir manualmente a máquina de estado

Navegue para a página do **Step Functions**. Se você nomeou as máquinas de estado de acordo com as instruções dadas:

- Selecione **InputOutputProcessingMachine** da lista de máquinas de estado.
- Clique no botão **Delete**.
- Confirme clicando em **Delete state machine** na caixa de diálogo que aparecer.

Se você escolheu nomes diferentes para sua máquina de estado, siga as instruções acima selecionando o nome da máquina de estado apropriado.

- Vá até a página do [CloudFormation](https://console.aws.amazon.com/cloudformation/home) no Console da AWS.
- Selecione a pilha (stack) com o nome `SFW-Module-6` (ou qualquer outro nome que você tenha escolhido para a pilha) e então clique em **Delete**.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Certifique-se de que a exclusão da stack seja concluída com êxito. 
