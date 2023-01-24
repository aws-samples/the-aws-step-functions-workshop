---
title: 'Surveiller les Express Workflows'
weight: 97
---

La surveillance des workflows Express nécessite l'utilisation d'outils différents de ceux que vous utilisez pour les workflows Standards. Au lieu d'utiliser les widgets Graph Inspector et Execution Event History comme vous le feriez avec des workflows standards, avec des workflows express comme `ParallelProcessingMachine`, vous utiliseriez CloudWatch pour la surveillance.

1. Accédez à la console Step Functions et sélectionnez `ParallelProcessingMachine`.
2. Tout l'historique d'exécution est envoyé à CloudWatch Logs. Utilisez les onglets `Surveillance` et `Journalisation` dans la console Step Functions pour gagner en visibilité sur les exécutions Express Workflow.
3. L'onglet `Surveillance` affiche six graphiques avec des métriques CloudWatch pour les erreurs d'exécution, l'exécution réussie, la durée d'exécution, la durée facturée, la mémoire facturée et les exécutions démarrées.
    ![](/static/img-fr/module-7/express-workflows-metrics.png)
4. Accédez à l'onglet `Journalisation` pour afficher les journaux récents et la configuration de la journalisation, avec un lien vers CloudWatch Logs.
    ![](/static/img-fr/module-7/express-workflows-logs.png)
5. Cliquez pour afficher le groupe de journaux Cloudwatch pour y voir l'historique détaillé.

::alert[**Félicitations !** Vous venez de surveiller les exécutions de votre workflow Step Functions Express.]{type="success"}