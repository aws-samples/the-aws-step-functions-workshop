---
title: 'Módulo 11 - Implementando com AWS SAM'
weight: 130
---

The [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/) é um open-source framework para criar aplicações sem servidor. Ele fornece sintaxe abreviada para expressar funções, APIs, bancos de dados e mapeamentos de fontes de eventos. Com apenas algumas linhas por recurso, você pode definir o aplicativo desejado e modelá-lo usando YAML. Durante a implantação, o SAM transforma e expande a sintaxe do SAM na sintaxe do [AWS CloudFormation](https://aws.amazon.com/cloudformation/) permitindo que você crie aplicações sem servidor com mais rapidez.

Neste módulo, você usará o AWS SAM para implementar uma aplicação que configura o API Gateway para acionar um fluxo de trabalho síncrono do Step Functions Express.

**Duração estimada: 30 minutos**