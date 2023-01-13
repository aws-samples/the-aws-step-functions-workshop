---
title: "Exécuter la machine à états"
weight: 113
---

- Cliquez sur **Démarrer l'exécution** et utilisez ce qui suit comme valeur d'entrée.
:::code{showCopyAction=true showLineNumbers=false language=json}
{
  "Comment": "I am very happy to learn about Step Functions!"
}
:::

- Inspectez l'**historique des événements d'exécution** pour afficher une liste d'événements et en trouver un appelé **TaskSucceeded**. Cliquez pour développer cet événement et vous devriez trouver le sentiment détecté pour votre commentaire.
- N'hésitez pas à exécuter à nouveau la machine à états avec d'autres valeurs d'entrée dans le champ `Comment` et à afficher les résultats de l'analyse des sentiments de Comprehend.

::alert[**Félicitations !** Vous avez terminé avec succès une intégration de service AWS SDK.]{type="success"}
