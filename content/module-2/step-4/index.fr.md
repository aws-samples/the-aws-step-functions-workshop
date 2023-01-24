---
title: "Démarrer l'exécution"
weight: 44
---

Maintenant, cliquez sur **Démarrer une exécution** sur cette machine à états en utilisant les valeurs suivantes :

::code[{ "message": "Bienvenue à re:Invent!", "timer_seconds": 5 }]{showCopyAction=true language="js"}

Accédez à l'historique des événements pour cette exécution. Vous remarquerez que le temps d'exécution de la tâche `Send SNS Message` est relativement rapide. La machine à états se poursuit dès que l'API SNS Publish est appelée.

![Résultats du module 2](/static/img-fr/module-2/results.png)

Dans ce cas, la tâche `Send SNS Message` s'est terminée en 255 ms. Passez en revue votre propre historique des événements d'exécution pour comparer les résultats.

::alert[**Félicitations!** Vous avez exécuté une machine à états à l'aide du modèle **Réponse à la requête**.]{type="success"}
