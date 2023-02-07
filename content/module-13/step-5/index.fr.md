---
title: "Examiner l'impact sur les coûts"
weight: 155
---

Le coût et les performances sont les principales raisons d'envisager l'imbrication des workflows Express dans les workflows Standard.

## Tarification pour les *workflows standard*

Les workflows standard sont facturés en fonction du nombre de transitions d'état requises pour exécuter une charge de travail. Step Functions compte une transition d'état à chaque fois qu'une étape de votre flux de travail s'exécute. Vous êtes facturé pour le nombre total de transitions d'état sur toutes vos machines d'état standard, y compris les tentatives.

## Tarification pour les *workflows express*

En revanche, les *Workflows Express* sont facturés en fonction du nombre de requêtes et de leur durée. La durée est calculée à partir du moment où votre *workflow* commence à s'exécuter jusqu'à ce qu'il se termine ou se termine autrement, arrondie aux 100 ms les plus proches, et la quantité de mémoire utilisée pour exécuter votre flux de travail, facturée en tranches de 64 Mo.

## Comparaison des prix

Déplacer les 4 étapes de tâche Lambda de notre *workflow* standard et les remplacer par un appel vers un *workflow* express imbriqué élimine 3 étapes de l'exécution de chaque machine d'état.

Supposons que vous ayez exécuté le *workflow* standard d'origine 1 000 fois dans la région de Virginie du Nord. Vous seriez facturé pour 3 000 transitions d'état de plus que le workflow modifié.

### Workflow d'origine

**Coût total** = `(nombre de transitions par exécution x nombre d'exécutions) x $0.000025`  
**Coût total** = `(3 X 1000) X 0.000025 = $0.075`  
(*Note: cela n'inclut pas les 4 000 transitions d'état incluses dans l'offre gratuite d'AWS chaque mois*)  

### Workflow express imbriqué

Au lieu de cela, nous sommes désormais facturés pour le workflow express. Supposons que chaque appel d'Express Workflow dure en moyenne 11 300 ms et n'utilise pas plus de 64 Mo de mémoire.

**Coût de durée** = `(Durée facturée moyenne ms / 100) * prix par 100 ms`  
**Coût d'exécution** = `$0.000001 par requête`  
**Coût total** = `(Coût d'exécution + coût de durée) x Nombre de requêtes`  

**Coût de durée** = `(11300 MS /100) * $ 0.0000001042 = $0.0000117746`  
**Coût d'exécution** = `$0.000001 par requête`  
**Coût total** = `($0.000001 + $0.0000117746) x 1000 = $0.01`  

Pour résumer, dans cet exemple, il coûte 7,5 fois plus chers de conserver ces étapes dans le workflow standard. Le déplacement des étapes qui ne nécessitent pas les garanties d'exécution d'un workflow standard vers un workflow express imbriqué peut entraîner des économies pour votre charge de travail.

### Comment la durée du workflow express affecte le coût

Les économies de coûts dépendent du nombre d'étapes que vous supprimez de votre *workflow* standard et de la durée du *workflow* *express imbriqué. Dans l'exemple, vous avez supprimé trois (3) transitions d'état en remplaçant quatre (4) étapes de tâche par une étape de workflow imbriquée. Les économies varieront en fonction de la durée du flux de travail imbriqué, comme vous pouvez le voir ci-dessous.

![Tableau de comparaison des coûts](/static/img/module-13/cost-comparison-by-duration.png)
