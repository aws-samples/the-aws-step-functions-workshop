---
title: 'Configuração'
weight: 132
---

:::alert{header="Important" type="warning"}
Siga as instruções nesta página apenas se você estiver executando este workshop em sua própria conta. Para pular estas instruções [clique aqui](../step-3).
:::

- Clique em `Lançar` link em qualquer uma das regiões na tabela abaixo para iniciar a implantação.
  | Região | Lançar stack |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **Leste dos EUA (Norte da Virginia)**  us-east-1 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-11&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_11.yml) |
  | **Europa (Irlanda)** eu-west-1 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-11&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_11.yml) |
  | **Ásia-Pacífico (Cingapura)** ap-southeast-1 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-11&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_11.yml) |
  |**Ásia-Pacífico (Sydney)**  ap-southeast-2 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-11&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_11.yml) |

- A localização do modelo do CloudFormation será preenchida automaticamente no campo `URL do Amazon S3` , conforme mostrado no diagrama abaixo. Clique em `Próximo`
  ![CloudFormation specify template](/static/img/setup/setup-cloudformation-specify-template.png)
- Na página _Especificar detalhes da pilha_ , _Nome da pilha_ será preenchido automaticamente para `SFW-Module-11`. você pode especificar um nome diferente, se desejar.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Clique em _Próximo_ duas vezes e na última página `Revisar`, role até o final. Clique na caixa de seleção  `se mostrado` e, em seguida, clique em `Criar Pilha`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Espere até que a pilha mostre o status `CREATE_COMPLETE` status.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)