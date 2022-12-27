---
title: 'Módulo 9 - Integrações de serviços do AWS SDK'
weight: 110
---

O AWS Step Functions se integra a muitos outros serviços da AWS. Você pode usar o Step Functions [AWS SDK service integrations](https://docs.aws.amazon.com/pt_br/step-functions/latest/dg/supported-services-awssdk.html) para chamar mais de 220 serviços da AWS diretamente da sua máquina de estado, oferecendo acesso a mais de 10.000 ações de API.

Para usar as integrações do AWS SDK, você especifica o nome do serviço e a chamada da API. Algumas integrações exigem parâmetros e você pode, opcionalmente, especificar um padrão de integração de serviços. Observe que a ação da API será camel case e os nomes dos parâmetros serão Pascal case. Você pode usar a Amazon States Language para especificar uma ação de API da AWS no campo Resource de um estado de tarefa. Para fazer isso, use a seguinte sintaxe:

`arn:aws:states:::aws-sdk:serviceName:apiAction.[serviceIntegrationPattern]`

**Exemplos**

- Para descrever instâncias do Amazon EC2, use a sintaxe: `arn:aws:states:::aws-sdk:ec2:describeInstances`. Isso retornará como saída o valor de retorno da chamada da API describeInstances do Amazon EC2.

- Para listar buckets no Amazon S3, use `arn:aws:states:::aws-sdk:s3:listBuckets`. Isso retornará como saída o valor de retorno da chamada da API listBuckets do Amazon S3.

- Para iniciar uma execução nested no Step Functions, use a sintaxe: `arn:aws:states:::aws-sdk:sfn:startExecution`.Em seguida, você adicionará StateMachineArn como um parâmetro. Isso retornará como saída o valor de retorno do fluxo de trabalho nested do Step Functions.

**Duração estimada: 10 minutos**
