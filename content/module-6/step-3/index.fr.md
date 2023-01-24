---
title: "Utiliser Workflow Studio pour créer une machine à états"
weight: 83
---

1. Accédez à [Step Functions](https://console.aws.amazon.com/states/home) dans votre console AWS. Assurez-vous d'être dans la bonne région AWS.

2. Cliquez sur le bouton **Créer une machine d'état**.

3. Sélectionnez `Concevoir visuellement votre flux de travail` comme méthode de création, sélectionnez le type `Standard` et cliquez sur **Suivant**.
   ![Studio](/static/img-fr/module-6/studio-selection.png)

4. Vous devriez voir le Workflow Studio :
   ![Studio Designer](/static/img-fr/module-6/studio-designer.png)

5. Entrez un `Commentaire` sur le côté droit :

```bash
Un exemple de workflow démontrant le traitement des entrées et des sorties.
```

6. Faites glisser et déposez l'action **AWS Lambda Invoke** de la section **Actions** sur le côté gauche vers le formulaire du concepteur à l'endroit où il est écrit `Faites glisser le premier état ici`.
   ![Lambda Invoke](/static/img-fr/module-6/lambda-invoke-state.png)

7. Configurez l'état.

- Dans l'onglet **Configuration** du designer, saisissez un nom pour cet état : `Invoquer HelloFunction`.
- Vous devriez avoir une fonction Lambda appelée `HelloFunction` déjà déployée sur votre compte.
- Configurez cet état pour appeler cette fonction. Recherchez le champ `Paramètres de l'API` et cliquez sur `Entrer le nom de la fonction`. Faites défiler la liste des menus jusqu'à ce que vous trouviez **HelloFunction:$LATEST**. Sélectionnez cette valeur.

![Configuration](/static/img-fr/module-6/configuration.png)

- Cliquez sur l'onglet `Entrée` et cochez la case `Filtrer l'entrée avec le chemin d'entrée`. Entrez `$.lambda` pour la valeur.

  ![Entrée de configuration](/static/img-fr/module-6/config-input.png)

- Cliquez sur l'onglet `Sortie` et cochez la case `Ajouter une entrée d'origine à la sortie à l'aide de ResultPath`. Sélectionnez `Combine original input with result`. Entrez la chaîne suivante comme filtre ResultPath : `$.data.lambdaresult`.
- Cochez la case `Filtrer la sortie avec le chemin de sortie` et entrez `$.data` pour la valeur.
  ![Sortie de configuration](/static/img-fr/module-6/config-output.png)
- Cliquez sur l'onglet `Gestion des erreurs`. Recherchez la section `Réessayer en cas d'erreur` et supprimez le `Retrier #1` par défaut en cliquant sur l'icône d'édition à droite et en faisant défiler vers le bas pour cliquer sur le bouton **Supprimer**.

  ![Supprimer Retrier](/static/img-fr/module-6/remove-retrier.png)

- Cliquez sur **Suivant** et passez en revue le code généré, puis cliquez à nouveau sur **Suivant**.
- Entrez le nom de la machine à états : `InputOutputProcessingMachine`. Pour le rôle d'exécution, choisissez un rôle existant : `InputOutputProcessingStepFunctionRole`

  ![Iam Role](/static/img-fr/module-6/name-iam-role.png)

- Laissez les autres valeurs par défaut et cliquez sur **Créer une machine d'état**.
