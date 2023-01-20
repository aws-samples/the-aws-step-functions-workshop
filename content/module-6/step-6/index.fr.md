---
title: 'Nettoyage'
weight: 86
---
:::alert{header="Important" type="warning"}
Suivez les instructions sur cette page si vous souhaitez nettoyer les ressources de votre propre compte. Les comptes Event Engine ne nécessitent pas de nettoyage.
:::

## Supprimer manuellement la machine d'état

Accédez à **Step Functions** dans la console AWS.
Si vous avez nommé les machines d'état conformément aux instructions fournies :

- Sélectionnez **InputOutputProcessingMachine** dans la liste des machines d'état.
- Cliquez sur le bouton **Supprimer**
- Confirmez en cliquant sur le bouton **Supprimer la machine d'état** dans la boîte de dialogue qui s'affiche.

- Accédez à la page [CloudFormation](https://console.aws.amazon.com/cloudformation/home) dans la console AWS.
- Sélectionnez la pile portant le nom `SFW-Module-6` (ou tout autre nom que vous avez choisi pour la pile), puis cliquez sur `Supprimer`.
   ![CloudFormation delete](/static/img-fr/setup/setup-cloudformation-delete.png)
- Assurez-vous que la suppression de la pile se termine avec succès.

