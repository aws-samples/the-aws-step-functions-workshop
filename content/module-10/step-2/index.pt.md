---
title: 'Configuração'
weight: 122
---

:::alert{header="Important" type="warning"}
Siga as instruções nesta página apenas se você estiver executando este workshop por conta própria. Para pular estas instruções [clique aqui](../step-3).
:::

- Clique no link "Iniciar" em qualquer uma das regiões da tabela abaixo para iniciar a implantação.
  | Region | Launch stack |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Iniciar](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |
  | **Europe (Ireland)** eu-west-1 | [Iniciar](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Iniciar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Iniciar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-10&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_10.yml) |

- A localização do modelo do CloudFormation será preenchida automaticamente no campo "URL do Amazon S3", conforme mostrado no diagrama abaixo. Clique em `Next`
  ![CloudFormation specify template](/static/img/setup/setup-cloudformation-specify-template.png)
- Na página _Specify stack details_, _Stack name_ seria preenchido automaticamente para `SFW-Module-10`. Você pode especificar um nome diferente, se desejar.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Clique em _Next_ duas vezes e na última página `Review`, role até o final. Clique na caixa de seleção `se mostrado` e, em seguida, clique em `Create Stack`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Espere até que a pilha mostre o status `CREATE_COMPLETE`.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)
