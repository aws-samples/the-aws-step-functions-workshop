---
title: 'Limpeza'
weight: 136
---

:::alert{header="Important" type="warning"}
Siga as instruções nesta página se desejar limpar recursos em sua própria conta. As contas do Event Engine não requerem limpeza.
:::

### Destrua recursos criados pelo SAM

Ao concluir o teste, você pode destruir o API Gateway e a máquina de estado usando o AWS SAM. Copie/cole o seguinte comando no terminal no diretório raiz do aplicativo.

```bash
sam delete
```

Quando o `sam delete` estiver completo, você verá a seguinte mensagem:
![SAM Delete](/static/img/module-11/sam-delete.png)

### Excluir a Pilha do CloudFormation

- Navegue até a página [CloudFormation](https://console.aws.amazon.com/cloudformation/home) no Console AWS.
- Selecione a pilha com o nome `SFW-Module-11` (ou qualquer nome que você escolheu para a pilha) e clique em Excluir. Isso limpará o ambiente AWS Cloud9 e quaisquer outros recursos relacionados na pilha.
  ![CloudFormation delete](/static/img/setup/setup-cloudformation-delete.png)
- Certifique-se de que a exclusão da pilha foi concluída com êxito.
