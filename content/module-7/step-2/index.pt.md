---
title: 'Configuração'
weight: 92
---

:::alert{header="Importante" type="warning"}
Siga as instruções nessa página **apenas** se você estiver executando esse workshop em sua própria conta. Para pular essas instruções, [clique aqui](../step-3).
:::

- Clique no link `Lançar` ao lado de qualquer uma das regiões na tabela abaixo para começar o provisionamento dos recursos.
  | Region | Lançar pilha |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |
  | **Europe (Ireland)** eu-west-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-7&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_7.yml) |

- A localização do modelo do CloudFormation será preenchida automaticamente no campo `Amazon S3 URL` como mostrado no diagrama abaixo. Clique em `Próximo`
  ![CloudFormation especificar template](/static/img/setup/setup-cloudformation-specify-template.png)
- Na página _Específicar detalhes_ da pilha, o campo _Nome da pilha_ será preenchido com o valor `SFW-Module-7`. Você pode especificar um nome diferente se você quiser.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Clique em _Next_ duas vezes e na última página `Review`, role até o final. Clique no checkbox `se ele for mostrado` e então clique em `Enviar`.
  ![CloudFormation criar stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Aguarde até que a pilha mostre o status `CREATE_COMPLETE`.
  ![CloudFormation stack completa](/static/img/setup/setup-cloudformation-create-complete.png)
