---
title: 'Módulo 10 - Deploy com o AWS CDK'
weight: 120
---

O [AWS Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/v2/guide/home.html) permite criar aplicativos na nuvem com o poder de uma linguagem de programação. O AWS CDK oferece suporte a TypeScript, JavaScript, Python, Java, C#/.Net e (na visualização do desenvolvedor) Go. Os desenvolvedores podem usar uma dessas linguagens de programação compatíveis para definir componentes de nuvem reutilizáveis ​​conhecidos como [Constructs](https://docs.aws.amazon.com/cdk/v2/guide/constructs.html). Você os compõe em [Stacks](https://docs.aws.amazon.com/cdk/v2/guide/stacks.html) e [Apps](https://docs.aws.amazon.com/cdk/v2/guide/apps.html).

![diagrama AWS CDK](/static/img/module-10/AppStacks.png)

Neste módulo, você usará o AWS CDK com TypeScript para implantar um aplicativo que configura o API Gateway para acionar um fluxo de trabalho síncrono do Step Functions Express.

**Duração Estimada: 30 minutos**