---
title: "Exécutez la machine à états et observez le résultat"
weight: 84
---

1. Cliquez sur la machine à états `InputOutputProcessingMachine` dans la console Step Functions.
2. Cliquez sur  **Démarrer une exécution** et utilisez le JSON ci-dessous comme entrée.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
   "comment": "Un commentaire d'entrée.",
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
3. Une fois l'exécution réussie, examinez la sortie dans l'onglet `Entreée et sortie de l'exécution`. Remarquez comment le contenu du bloc `"data"` dans l'entrée JSON est ajouté à la sortie de la fonction Lambda. Cette sortie serait transmise à l'état suivant de votre workflow.

::alert[**Félicitations!** Vous avez exécuté une machine à états utilisant les fonctionnalités de traitement des données d'entrée et de sortie.]{type="success"}