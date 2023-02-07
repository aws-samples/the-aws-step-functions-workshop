---
title: 'Mise en place'
weight: 152
---

:::alert{header="Important" type="warning"}
Suivez les instructions sur cette page uniquement si vous exécutez cet atelier dans votre propre compte. Pour ignorer ces instructions [cliquez ici](../step-3).
:::

- Cliquez sur le lien `Lancer` dans l'une des régions du tableau ci-dessous pour démarrer le déploiement.
  | Region |  |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-12&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_13.yml) |
  | **Europe (Ireland)** eu-west-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-12&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_13.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-12&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_13.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Lancer](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-12&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_13.yml) |

- L'emplacement du modèle CloudFormation sera renseigné automatiquement dans le champ `URL Amazon S3`, comme indiqué dans le schéma ci-dessous. Cliquez sur `Suivant`
  ![CloudFormation spécifie le modèle](/static/img-fr/module-12/setup-cloudformation-specify-template.png)
- Sur la page _Spécifier les détails de la pile_, _Nom de la pile_ serait automatiquement renseigné sur `SFW-Module-12`. Vous pouvez spécifier un nom différent si vous le souhaitez.
  ![Nom de la pile CloudFormation](/static/img-fr/module-12/setup-cloudformation-stack-name.png)
- Cliquez deux fois sur _Suivant_ et sur la dernière page "Révision", faites défiler vers le bas. Cochez la case "si affiché", puis cliquez sur "Créer une pile".
  ![CloudFormation crée une pile](/static/img-fr/module-12/setup-cloudformation-create-stack.png)
- Attendez que la pile affiche l'état `CREATE_COMPLETE`.
  ![Pile CloudFormation terminée](/static/img-fr/setup/setup-cloudformation-create-complete.png)
