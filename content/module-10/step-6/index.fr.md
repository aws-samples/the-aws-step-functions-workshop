---
title: 'Nettoyer'
weight: 126
---

:::alert{header="Important" type="warning"}
Suivez les instructions sur cette page si vous souhaitez nettoyer les ressources de votre propre compte AWS. Les comptes fournis par AWS dans un atelier dirigé ne nécessitent pas de nettoyage.
:::

### Détruire les ressources créées par CDK

Une fois les tests terminés, vous pouvez détruire la passerelle API et la machine à états à l'aide d'AWS CDK. Copiez/collez la commande suivante dans le terminal dans le répertoire racine de l'application.

```bash
cdk destroy
```

Lorsque le `cdk destroy` est terminé, vous verrez le message suivant :
![CDK Destroy](/static/img/module-10/cdk-destroy.png)

### Supprimer la pile CloudFormation

- Accédez à la page [CloudFormation](https://console.aws.amazon.com/cloudformation/home) dans la console AWS.
- Sélectionnez la pile avec le nom `SFW-Module-11` (ou tout nom que vous avez choisi pour la pile), puis cliquez sur **Supprimer**. Cela nettoiera l'environnement AWS Cloud9 et toutes les autres ressources associées dans la pile.
  ![Supprimer la pile CloudFormation](/static/img-fr/setup/setup-cloudformation-delete.png)
- Assurez-vous que la suppression de la pile se termine avec succès.
