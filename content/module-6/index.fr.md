---
title: 'Module 6 - Traitement des entrées et des sorties'
weight: 80
---
Une exécution de Step Functions reçoit du JSON en entrée et transmet cette entrée au premier état du workflow. Chaque état reçoit du JSON en entrée et transmet généralement du JSON en sortie à l'état suivant. Comprendre comment ces informations circulent d'un état à l'autre et apprendre à filtrer et à manipuler ces données est essentiel pour concevoir et mettre en œuvre des workflows efficaces dans Step Functions.

Dans le format ASL, ces champs filtrent et contrôlent le flux de JSON d'un état à l'autre :

- `InputPath`
- `OutputPath`
- `ResultPath`
- `Parameters`
- `ResultSelector`

Lisez la documentation pour en savoir plus sur le [traitement des entrées et des sorties](https://docs.aws.amazon.com/fr_fr/step-functions/latest/dg/concepts-input-output-filtering.html).

**Durée estimée : 25 minutes**