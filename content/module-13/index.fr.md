---
title: 'Module 13 - Workflows imbriqués'
weight: 150
---

Les *workflows* imbriqués sont utiles lorsque vous souhaitez regrouper des parties d'une machine à états, par exemple pour les réutiliser en tant que bloc de construction dans plusieurs *workflows*. Mais les *workflows* imbriqués vous permettent également de mélanger les *workflows* Standard et Express. Les *workflows* express sont souvent moins coûteux que le *workflows* standard équivalent, mais il est important de comprendre les différences entre eux. Votre *workflows* peut contenir certaines étapes qui nécessitent des fonctionnalités non disponibles avec les *workflows* Express, telles que les méthodes d'appel `.waitForTaskToken` et `.sync`, ou votre *workflows* peut s'exécuter pendant plus de 5 minutes. Ou, vous pourriez avoir besoin d'un modèle d'exécution de *workflows* "*at least once*". Dans ce cas, ces étapes feraient partie d'un *workflow* standard.

Cependant, certaines étapes peuvent être idempotentes, ce qui signifie qu'elles doivent être exécutées plusieurs fois sans affecter le résultat final. Ces étapes fonctionneraient bien dans un *workflow* Express, avec son modèle de livraison "*at least once*". Ces étapes peuvent être extraites de votre *workflow* Standard et placées dans un *workflow* Express imbriqué. Cela pourrait améliorer les performances et réduire les coûts. Ce module vous montrera comment procéder.

Consulter la documentation:

- [Standard vs. Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)

**Durée estimée : 20 minutes**
