---
title: 'Configuração'
weight: 92
---

:::alert{header="Importante" type="warning"}
Siga as instruções nessa página **apenas** se você estiver executando esse workshop em sua própria conta. Para pular essas instruções, [clique aqui](../step-3).
:::

- Clique no link de `Launch` ao lado de qualquer uma das regiões na tabela abaixo para começar o provisionamento dos recursos.
  | Region | Launch stack |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |
  | **Europe (Ireland)** eu-west-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |

- A localização do modelo do CloudFormation será preenchida automaticamente no campo `URL do Amazon S3`, conforme mostrado no diagrama abaixo. Clique em `Próximo`.
  ![CloudFormation specify template](/static/img/setup/setup-cloudformation-specify-template.png)
- Na página _Especificar detalhes da pilha_, o _Nome da pilha_ será autopreenchido com `SFW-Module-6`. Você pode especificar um nome diferente se quiser.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Clique _Próximo_ mais duas vezes e na última página `Revisar`, role até o final da página. Clique na caixa de seleção `se houver` e então clique `Criar pilha`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Espere até o estado da pilha mudar para `CREATE_COMPLETE`.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)
