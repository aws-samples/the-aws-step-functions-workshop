---
title: 'Limpeza'
weight: 126
---

:::alert{header="Importante" type="warning"}
Siga as instruções nesta página se desejar limpar recursos em sua própria conta. As contas do Event Engine não requerem limpeza.
:::

### Exclua recursos criados pelo CDK

Ao concluir o teste, você pode excluir o API Gateway e a máquina de estado usando o AWS CDK. Copie/cole o seguinte comando no terminal no diretório raiz do aplicativo.

```bash
cdk destroy
```

Quando o `cdk destroy` estiver completo, você verá a seguinte mensagem:
![CDK Destroy](/static/img/module-10/cdk-destroy.png)

### Excluir stack do CloudFormation

- Navegue até a página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) no Console AWS.
- Selecione a stack com o nome `SFW-Module-10` (ou qualquer nome que você escolheu para a stack) e clique em Excluir. Isso limpará o ambiente AWS Cloud9 e quaisquer outros recursos relacionados na stack.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Certifique-se de que a exclusão da pilha foi concluída com êxito.
