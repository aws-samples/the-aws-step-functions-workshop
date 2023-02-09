---
title: 'Módulo 13 - Fluxos de Trabalho Aninhados'
weight: 150
---
À medida que você ganha mais experiência com o Step Functions e a complexidade de suas máquinas de estado aumenta, você pode começar a procurar maneiras de simplificar e otimizar as execuções de suas máquinas de estados. Aninhar fluxos de trabalho dentro de outros fluxos de trabalho é uma ferramenta poderosa. Do ponto de vista da modularidade, os fluxos de trabalho aninhados permitem criar máquinas de estado reutilizáveis que podem ser executadas por outros fluxos de trabalho, promovendo a reutilização. O agrupamento de fluxos de trabalho de diferentes tipos, como um fluxo de trabalho Express aninhado dentro de um fluxo de trabalho Standard, pode ajudar você a reduzir custos. Para fluxos de trabalho Standard, você paga por transição de estado, e fluxos de trabalho grandes e complexos podem se tornar caros em grande escala. Uma forma de reduzir custos é determinar se alguma etapa pode ser movida para um fluxo de trabalho Express. Diferentemente dos fluxos de trabalho Standard, os fluxos de trabalho Express são cobrados pelo tempo de execução, independentemente do número de transições de estado e do custo por execução.

Os fluxos de trabalho Express diferem dos fluxos de trabalho Standard de algumas maneiras importantes:

1. Os fluxos de trabalho Standard têm um modelo de execução “exatamente uma vez”, enquanto os fluxos de trabalho Express são “pelo menos uma vez”.
1. Os fluxos de trabalho Express não oferecem suporte a determinados métodos de invocação, como `sync` e `waitForTaskToken`.
1. Os fluxos de trabalho Express têm uma duração máxima de 5 minutos, enquanto os fluxos de trabalho Standard podem ser executados por até 365 dias.

Para uma comparação completa dos fluxos de trabalho Standard e Express, consulte a [documentação] (https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html).

Ao examinar seus fluxos de trabalho, você pode identificar etapas que poderiam ser movidas para um fluxo de trabalho Express, talvez porque elas sejam [idempotentes] (https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-idempotent/), o que significa que elas podem ser executadas mais de uma vez sem afetar o resultado final. Nesse caso, você pode criar um fluxo de trabalho Express contendo essas etapas e, em seguida, executar esse fluxo de trabalho aninhado de dentro do seu fluxo de trabalho Standard existente, obtendo economias de custos ao fazer isso.

Este módulo guiará você pelo processo usando o console da AWS, mas você também pode desenvolver fluxos de trabalho aninhados escritos em [Amazon States Language (ASL)] (https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) e implantados usando [AWS CloudFormation] (https://aws.amazon.com/cloudformation/) ou o [AWS Serverless Application Model (SAM)] (https://aws.amazon.com/serverless/sam/), usando o [AWS Cloud Development Kit (CDK)] (https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_stepfunctions_tasks.StepFunctionsStartExecution.html ), ou usando ferramentas de infraestrutura como código (IaC) de terceiros, como o Terraform e o Serverless Framework.

Revise a documentação:

- [Fluxos de Trabalho Standard vs. Express](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Optimização de custos usando Fluxos de Trabalho Express](https://docs.aws.amazon.com/step-functions/latest/dg/cost-opt-exp-workflows.html)
- [Construindo Fluxos de Trabalho com efetividade de custo usando AWS Step Functions](https://aws.amazon.com/blogs/compute/building-cost-effective-aws-step-functions-workflows/)
- [Exemplo de verificaçao seletiva](https://docs.aws.amazon.com/step-functions/latest/dg/sample-project-express-selective-checkpointing.html)

**Duração estimada: 20 minutos**