---
title: "Mise en place"
weight: 31
---

:::alert{header="Important" type="warning"}
Suivez les instructions sur cette page uniquement si vous exécutez cet atelier dans votre propre compte AWS. Pour ignorer ces instructions, [cliquez ici](../step-2).
:::

- Cliquez sur le lien **Lancer** dans l'une des régions du tableau ci-dessous pour démarrer le déploiement des ressources.
  | Région | Déploiement |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Europe (Ireland)** eu-west-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Canada (Central)** ca-central-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |

- L'emplacement du modèle CloudFormation sera renseigné automatiquement dans le champ `URL Amazon S3`, comme indiqué dans le schéma ci-dessous. Cliquez sur **Suivant**.
  ![Choix du modèle CloudFormation](/static/img-fr/setup/setup-cloudformation-specify-template.png)
- Dans la page `Spécifier les détails de la pile`, le champ `Nom de la pile` devrait être `SFW-Module-1`. Vous pouvez spécifier un nom différent si vous le souhaitez.
  ![Choix du nom de la pile CloudFormation](/static/img-fr/setup/setup-cloudformation-stack-name.png)
- Cliquez deux fois sur **Suivant**, et sur la page intitulée `Vérifier`, faites défiler vers le bas puis cochez la case `Je sais qu’AWS CloudFormation peut créer des ressources IAM`, puis cliquez sur `Soumettre`.
  ![Création de la pile CloudFormation](/static/img-fr/setup/setup-cloudformation-create-stack.png)
- Attendez que la pile affiche l'état `CREATE_COMPLETE`.
  ![Pile CloudFormation prête](/static/img-fr/setup/setup-cloudformation-create-complete.png)
