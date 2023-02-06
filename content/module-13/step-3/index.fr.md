---
title: "Présentation de la machine d'état"
weight: 153
---

Dans votre compte, vous avez une machine d'état dont le nom commence par _ParentStateMachine_. La machine d'état est actuellement un *workflow* standard. Comme mentionné au début du module, les *workflow* standards peuvent être nécessaire si vous utilisez une fonctionnalité disponible uniquement pour *workflow* standard, comme la fonctionnalité `.waitForTaskToken`, ou parce que la durée du *workflow* peut dépasser 5 minutes, ou parce que vous avez besoin d'un modèle d'execution "*at least once*".

Cependant, notez les étapes encerclées ci-dessous. Supposons que ces étapes sont idempotentes et conviendraient à un modèle d'exécution "*at least once*", comme celui fourni par les Express workflows, alors nous pourrions déplacer ces étapes vers un workflow Express imbriqué.

![Étapes susceptibles d'utiliser un workflow Express](/static/img/module-13/state-machine-express-step-candidates.png)
