---
title: "Créer la machine à états et provisionner les ressources"
weight: 112
---

1. Accédez à [Step Functions](https://console.aws.amazon.com/states/home) dans votre console AWS. Assurez-vous d'être dans la bonne région.

2. Si vous n'êtes pas sur la page `Machines d'état`, cliquez sur **Machines d'état** dans le menu de gauche et cliquez sur **Créer une machine d'état**

3. Pour `Choisir la méthode de création`, sélectionnez **Concevoir visuellement votre flux de travail**, sélectionnez **Standard** comme `Type` de la machine à états et cliquez sur **Suivant**.
   ![Studio](/static/img-fr/module-6/studio-selection.png)

4. Vous devriez maintenant voir le studio de design qui ressemblera à ceci.
   ![](/static/img-fr/module-6/studio-designer.png)

5. Entrez un `Commentaire` sur le côté droit :

```bash
Un workflow qui contient une intégration avec Amazon Comprehend grâce au AWS SDK.
```

6. Dans le menu **Actions** de gauche, utilisez la barre de recherche et recherchez `DetectSentiment`. Vous devriez voir apparaître l'action **Comprehend DetectSentiment**.

7. Faites glisser et déposez `DetectSentiment` de la section **Actions** sur le côté gauche du designeur vers la où il est écrit `Faites glisser le premier état ici`.
   ![](/static/img-fr/module-9/detect-sentiment.png)
   ![](/static/img-fr/module-9/detect-sentiment-state.png)

8. Cliquez sur l'action **Comprehend: DetectSentiment**
9. Mettez à jour les `Paramètres de l'API` dans l'onglet **Configuration** pour utiliser les éléments suivants :
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "LanguageCode": "en",
  "Text.$": "$.Comment"
}
:::

    La machine à états transmettra la valeur `Comment` de l'entrée d'exécution à Comprehend pour l'analyse des sentiments.

10. Utilisez les valeurs par défaut pour **Entrée, Sortie et Gestion des erreurs**. Cliquez sur le bouton **Définition** pour revoir la syntaxe ASL que vous allez générer.

11. Cliquez maintenant sur **Suivant** et passez en revue le code généré. Cliquez à nouveau sur **Suivant**.

12. Donnez un nom à votre machine à états, `DetectSentimentMachine`.

13. Cliquez sur le bouton **Choisir un rôle existant** et sélectionnez `UniversalSDKRoleNameforStepfunctions` dans le menu déroulant.

![](/static/img-fr/module-9/iam.png)

14. Cliquez maintenant sur **Créer une machine d'état**.

Vous avez créé la machine à états avec succès.
