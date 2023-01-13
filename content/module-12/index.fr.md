---
title: 'Module 12 - Observabilité'
weight: 140
---
L'observabilité vous aide à comprendre ce qui se passe dans vos systèmes et applications. L'observabilité vous aide à détecter, étudier et résoudre les problèmes.

Les trois piliers de l'observabilité sont :
  - Métriques
  - Journaux
  - Traces

*Metrics* sont une représentation numérique des données mesurées sur des intervalles de temps. Les métriques fournissent des données sur les performances de vos systèmes. Vous pouvez considérer une métrique comme une variable unique utilisée pour surveiller un aspect de votre système. Lorsque vous combinez toutes ces métriques individuelles, vous êtes en mesure de voir les performances de votre application au fil du temps.

Les *journaux* vous aident à suivre les événements qui se sont produits dans votre application ou votre système. Les journaux sont des enregistrements horodatés qui peuvent inclure des événements tels que des échecs, des erreurs, des transformations d'état ou même qui a accédé à votre système à un certain moment. Les journaux peuvent être enregistrés dans des formats non structurés, semi-structurés ou structurés.

Les *traces* sont des représentations d'une série d'événements distribués causalement liés. Les traces peuvent representer les flux de requêtes d'un système distribué de bout en bout.

Les métriques de surveillance, les journaux et les traces peuvent vous aider à comprendre la disponibilité, les performances et la santé de vos applications. AWS fournit plusieurs outils que vous pouvez utiliser avec Step Functions pour surveiller ces trois piliers de l'observabilité.

Consultez la documentation :
- [Journalisation et surveillance dans AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/monitoring-logging.html)
- [Suivi de l'état d'exécution à l'aide d'Amazon EventBridge](https://docs.aws.amazon.com/step-functions/latest/dg/cw-events.html)
- [AWS X-Ray et Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html)

**Durée estimée : 30 minutes**
