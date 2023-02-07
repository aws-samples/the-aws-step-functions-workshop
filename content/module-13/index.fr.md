---
title: 'Module 13 - Workflows imbriqués'
weight: 150
---

Au fur et à mesure que vous acquérez plus d'expérience avec Step Functions et que la complexité de vos machines d'état augmente, vous pouvez commencer à chercher des moyens de simplifier et d'optimiser leurs exécutions. L'imbrication de *workflow* dans d'autres *workflow* est un outil puissant. Du point de vue de la modularité, les *workflow* imbriqués vous permettent de créer des machines d'état réutilisables qui peuvent être exécutées par d'autres *workflow*, favorisant ainsi la réutilisation. L'imbrication de *workflow* de différents types, comme un *workflow* Express imbriqué dans un *workflow* Standard, peut vous aider à réduire les coûts. Pour les *workflow* standard, vous payez par transition d'état, et les flux de travail volumineux et complexes peuvent devenir coûteux à grande échelle. Une façon de réduire les coûts consiste à déterminer si des étapes peuvent être déplacées vers un *workflow* Express. Contrairement aux *workflow* standard, les *workflow* express sont facturés pour la durée de leur exécution, quel que soit le nombre de transitions d'état, ainsi qu'un coût par exécution.

Les *workflow* express diffèrent des *workflow* standard de plusieurs manières importantes :

1. Les *workflow* standard ont un modèle d'exécution "exactement une fois", tandis que les *workflow* express sont "au moins une fois".
1. Les *workflow* express ne prennent pas en charge certaines méthodes d'appel, telles que `sync` et `waitForTaskToken`.
1. Les *workflow* express ont une durée maximale de 5 minutes, tandis que les *workflow* standard peuvent s'exécuter jusqu'à 365 jours.

Pour une comparaison complète des *workflow* Standard et Express, veuillez vous référer à la [documentation](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-standard-vs-express.html).

Lorsque vous examinez vos *workflow*, vous pouvez identifier les étapes qui pourraient être déplacées dans un *workflow* Express, peut-être parce qu'elles sont [idempotentes](https://aws.amazon.com/fr/premiumsupport/knowledge-center/lambda-function-idempotent/?nc1=h_ls), ce qui signifie qu'ils peuvent être exécutés plusieurs fois sans affecter le résultat final. Dans ce cas, vous pouvez créer un *workflow* Express contenant ces étapes, puis exécuter ce *workflow* imbriqué à partir de votre *workflow* Standard existant, ce qui vous permet de réaliser des économies.

Ce module vous guidera tout au long du processus à l'aide de la console AWS, mais vous pouvez également développer des *workflow* imbriqués écrits en [Amazon States Language (ASL)](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-amazon-states-language.html) et déployé à l'aide de [AWS CloudFormation](https://aws.amazon.com/fr/cloudformation/) ou du [AWS Serverless Application Model (SAM)](https://aws.amazon.com/fr/serverless/sam/), à l'aide du [AWS Cloud Development Kit (CDK)](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_stepfunctions_tasks.StepFunctionsStartExecution.html), ou en utilisant des outils tiers d'*infrastructure as code* (IaC) comme Terraform et Serverless Framework.

Consultez la documentation :

- [*workflow* standard ou express](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Optimisation des coûts à l'aide de *workflow* express](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/cost-opt-exp-workflows.html)
- [Création de *workflow* AWS Step Functions efficaces](https://aws.amazon.com/fr/blogs/compute/building-cost-effective-aws-step-functions-workflows/)
- [Exemple de point de contrôle sélectif](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/sample-project-express-selective-checkpointing.html)

**Durée estimée : 20 minutes**
