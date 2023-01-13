---
title: 'Utiliser le simulateur de flux de données pour tester le traitement des données'
weight: 85
---

1. Cliquez sur le bouton `Simulateur de flux de données` dans la zone `Affichage du graphique`

Le simulateur de flux de données permet aux développeurs de simuler l'ordre de traitement des données qui se produit dans un état lors de l'exécution. Cela aide les développeurs à comprendre comment filtrer et manipuler les données lorsqu'elles circulent d'un état à l'autre. Les développeurs peuvent spécifier une entrée JSON de départ et l'évaluer à travers chacune des étapes du traitement.

Le simulateur démarre à l'étape `State Input`. Le champ de saisie valide automatiquement l'objet JSON et met en évidence les éventuelles erreurs de syntaxe.

![Simulateur de flux de données](/static/img-fr/module-6/simulator.png)

2. Utilisez le simulateur de flux de données pour tester le traitement des données d'entrée pour le workflow `InputOutputProcessingMachine`. Remplacez l'entrée d'état par défaut par le JSON ci-dessous et choisissez l'étape `InputPath`. Utilisez `$.lambda` pour l'InputPath.

:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "An input comment.",
   "data": {
      "value1": 23,
      "value2": 17
   },
   "extra": "foo",
   "lambda": {
      "who": "AWS Step Functions"
   }
}
:::

![Simulateur de flux de données](/static/img-fr/module-6/input-path.png)

Le panneau de gauche affiche l'entrée d'état avant l'application de `InputPath`. Le panneau de droite affiche l'entrée d'état après l'application de `InputPath`.

Les développeurs peuvent utiliser le simulateur de flux de données pour implémenter rapidement le traitement de données dont ils ont besoin dans leurs machines d'état.
N'hésitez pas à continuer à tester les valeurs de `ResultSelector` et `OutputPath` dans le simulateur de flux de données.

Pour plus d'informations sur le simulateur de flux de données, consultez cet [article de blog](https://aws.amazon.com/blogs/compute/modeling-workflow-input-output-path-processing-with-data-flow-simulator/).

::alert[**Félicitations!** Vous avez utilisé le simulateur de flux de données pour tester le traitement des données d'entrée et de sortie avec Amazon States Language !]{type="success"}

# Utilisation des fonctions intrinsèques pour accélérer votre traitement de données

L'Amazon States Language (ASL) fournit plusieurs fonctions intrinsèques, qui vous aident à effectuer des opérations de traitement de données de base sans utiliser d'état `Task`.
Des exemples d'opérations incluent les opérations mathématiques, la création d'ID uniques ou la fusion d'objets JSON. Vous pouvez utiliser des fonctions intrinsèques comme `States.MathAdd`, `States.UUID` ou `States.JsonMerge` dans votre *workflow* pour éviter la surcharge d'une fonction Lambda pour effectuer ces opérations.

Pour une liste complète des fonctions intrinsèques, consultez la page de documentation [ici](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/amazon-states-language-intrinsic-functions.html).

Dans cette section, vous utiliserez la fonction intrinsèque `States.MathAdd` pour additionner deux nombres sans avoir besoin d'utiliser une fonction Lambda pour effectuer l'opération.
1. Revenez à Workflow Studio sur la machine d'état `InputOutputProcessingMachine`.
2. Ajoutez un nouvel état `Pass` à la machine d'état après l'état `Lambda Invoke`. Notez que vous n'êtes pas limité aux états `Pass` pour les fonctions intrinsèques, vous pourrez les utiliser dans n'importe quel état prenant en charge ces fonctions.

![Etat Pass valeur d'entrée](/static/img/module-6/pass-state-diagram.png)

3. Dans l'onglet Input de l'état Pass, remplissez la valeur suivante dans le champ de texte du paramètre. Notez que vous devrez ajouter le suffixe `.$` lors de l'utilisation d'intrinsèques.
    ```json
      {
        "Sum.$": "States.MathAdd($.value1, $.value2)"
      }
    ```

![Etat Pass valeur d'entrée](/static/img-fr/module-6/pass-state-input-intrinsic.png)

4. Cliquez sur **Démarrer une exécution** et utilisez le JSON ci-dessous comme charge utile d'entrée.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "An input comment.",
   "data": {
      "value1": 23,
      "value2": 17
   },
   "extra": "foo",
   "lambda": {
      "who": "AWS Step Functions"
   }
}
:::
5. Une fois l'exécution réussie, examinez la sortie dans l'onglet "Sortie d'exécution". Vous verrez que le champ `sum` a la somme de value1 et value2 vennant des valeurs d'entrées.

![Sortie d'execution](/static/img/module-6/intrinsic-execution-output.png)

::alert[**Félicitations !** Vous avez utilisé une fonction intrinsèque pour effectuer un traitement de base des données sans avoir à écrire de code !]{type="success"}