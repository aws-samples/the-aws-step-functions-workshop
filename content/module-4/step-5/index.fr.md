---
title: 'Implémentez le rappel'
weight: 65
---

Accédez au [service Lambda dans la console](https://console.aws.amazon.com/lambda/home) et recherchez la fonction dont le nom contient la chaîne **CallbackWithTaskToken**. C'est la fonction qui est responsable du traitement des messages ajoutés à la file d'attente SQS. Vous modifierez cette fonction pour implémenter un rappel.

Passez en revue le code et notez que la fonction Lambda reçoit le `TaskToken` de SQS et peut le renvoyer à la machine à états en tant que paramètre de la méthode `.sendTaskSuccess`.

Décommentez le code indiqué dans l'image ci-dessous et cliquez sur le bouton **Déployer**.

![Code à décommenter](/static/img/module-4/lambda.png)


