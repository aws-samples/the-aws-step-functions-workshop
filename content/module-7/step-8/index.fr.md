---
title: 'Nettoyer'
weight: 98
---

:::alert{header="Important" type="warning"}
Suivez les instructions sur cette page si vous souhaitez nettoyer les ressources de votre propre compte AWS. Les comptes fournis par AWS dans un atelier dirigé ne nécessitent pas de nettoyage.
:::

### Supprimer manuellement la machine à états

Accédez à `Step Functions`
Si vous avez nommé les machines d'état conformément aux instructions fournies :

- Sélectionnez `ParallelProcessingMachine` dans la liste des machines d'état.
- Cliquez sur le bouton **Supprimer**
- Confirmez en cliquant sur le bouton **Supprimer la machine d'état** dans la boîte de dialogue qui s'affiche.
  ![Suppression de la machine à états](/static/img-fr/module-7/manual-delete-sm.png)

Si vous avez choisi des noms différents pour votre machine à états, suivez les instructions ci-dessus tout en sélectionnant le nom approprié.

- Accédez à la page [CloudFormation](https://console.aws.amazon.com/cloudformation/home) dans la console AWS.
- Sélectionnez la pile portant le nom `SFW-Module-7` (ou tout autre nom que vous avez choisi pour la pile), puis cliquez sur **Supprimer**.
  ![Supprimer la pile CloudFormation](/static/img-fr/setup/setup-cloudformation-delete.png)
- Assurez-vous que la suppression de la pile se termine avec succès.

### Supprimer manuellement le groupe de journaux CloudWatch

Accédez à [CloudWatch](https://console.aws.amazon.com/cloudwatch/home). Cliquez sur `Journaux` dans la navigation et sélectionnez `Groupes de journaux`.

- Sélectionnez le groupe de journaux appartenant à `ParallelProcessingMachine`.
- Cliquez sur le menu déroulant **Actions**, puis sélectionnez `Supprimer le(s) groupe(s) de journaux`.
  ![Cloudwatch loggroup delete](/static/img-fr/module-7/cloudwatch-cleanup.png)
- Confirmez en cliquant sur le bouton **Supprimer** dans le dialogue contextuel.
