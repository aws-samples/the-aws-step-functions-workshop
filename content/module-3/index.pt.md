---
title: 'Módulo 3 - Executar um trabalho (.sync)'
weight: 50
---

Para serviços integrados, como AWS Batch e Amazon ECS, o Step Functions pode aguardar a conclusão de uma tarefa antes de avançar para o próximo estado. Esse padrão de orquestração de tarefas é chamado [Execução de trabalho (.sync)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html#connect-sync) na documentação. Para ver uma lista dos serviços integrados que oferecem suporte à sincronização, consulte [Integrações otimizadas para Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).

Para ver um exemplo de projeto de computação de alto desempenho (HPC) usando AWS Batch, Step Functions e Executar um trabalho (.sync), veja [esta postagem do blog](https://aws.amazon.com/blogs/compute/orchestrating-high-performance-computing-with-aws-step-functions-and-aws-batch/).

Neste módulo, você configurará e executará uma tarefa sincronizada usando **Execução de trabalho (.sync)**.

**Duração Estimada: 10 minutos**
