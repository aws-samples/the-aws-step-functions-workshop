---
title: 'Configuração'
weight: 42
---

:::alert{header="Importante" type="warning"}
Siga as instruções nesta página apenas se você estiver executando este workshop em sua própria conta. Para pular estas instruções [clique aqui](../step-3).
:::

- Clique no link `Lançar` em qualquer uma das regiões na tabela abaixo para iniciar a implantação.
  | Região | Lançar a stack |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **Leste dos EUA (Norte da Virginia)** us-east-1 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-2&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_2.yml) |
  | **Europa (Irlanda)** eu-west-1 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-2&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_2.yml) |
  | **Ásia-Pacífico (Cingapura)** ap-southeast-1 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-2&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_2.yml) |
  | **Ásia-Pacífico (Sydney)** ap-southeast-2 | [Lançar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-2&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_2.yml) |

- A localização do modelo do CloudFormation será preenchida automaticamente no campo `Amazon S3 URL` como mostrado no diagrama abaixo. Clique em `Next`
  ![CloudFormation especificar template](/static/img/setup/setup-cloudformation-specify-template.png)
- Na página _Específicar detalhes_ da stack, o campo _Stack name_ será preenchido com o valor `SFW-Module-2`. Você pode especificar um nome diferente se você quiser.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Clique em _Next_ duas vezes e na última página `Review`, role até o final. Clique no checkbox `se ele for mostrado` e então clique em `Create stack`.
  ![CloudFormation criar stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Aguarde até que a stack mostre o status `CREATE_COMPLETE`.
  ![CloudFormation stack completa](/static/img/setup/setup-cloudformation-create-complete.png)