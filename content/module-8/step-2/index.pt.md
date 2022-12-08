---
title: 'Configuração'
weight: 101
---

:::alert{header="Important" type="warning"}
Siga as instruções dessa página apenas se você estiver executando esse workshop na sua própria conta. Para pular essas instruções [clique aqui](../step-3).
:::

- Clique em `Lançar` link em qualquer uma das regiões na tabela abaixo para iniciar a implantação.
  | Região | Lançar stack |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **Leste dos EUA (Norte da Virginia)** us-east-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-8&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_8.yml) |
  | **Europa (Irlanda)** eu-west-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-8&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_8.yml) |
  | **Ásia-Pacífico (Cingapura)** ap-southeast-1 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-8&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_8.yml) |
  | **Ásia-Pacífico (Sydney)** ap-southeast-2 | [Launch](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-8&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_8.yml) |

- A localização do modelo do CloudFormation será preenchida automaticamente no campo `Amazon S3 URL` como mostrado no diagrama abaixo. Clique `Próximo`
  ![CloudFormation specify template](/static/img/setup/setup-cloudformation-specify-template.png)
- Na página _Especificar detalhes da pilha_, o nome da pilha seria preenchido automaticamente para `SFW-Module-8`. Você pode especificar um nome diferente, se desejar.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Clique em _Próximo_ duas vezes e na última página `Revisão`, role até o final. Clique na caixa de seleção `se mostrado` e, em seguida, clique em `Criar pilha`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Espere até que a pilha mostre o status `CREATE_COMPLETE`.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)
