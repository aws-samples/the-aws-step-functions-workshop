---
title: 'Remplacer les étapes par un Express workflow imbriqué'
weight: 154
---

Un workflow Express contenant ces étapes a déjà été créé dans votre compte, avec un nom commençant par _ChildStateMachine_.

1. Dans la [console Step Functions](https://console.aws.amazon.com/states/home), sélectionnez "Machines d'état" sur le côté gauche, puis cliquez sur la machine d'état dont le nom commence par *ChildStateMachine*. Dans la case "Détails" en haut, copiez la valeur ARN, car vous l'utiliserez dans une étape ultérieure.  

2. Ensuite, ouvrez la machine d'état dont le nom commence par *ParentStateMachine*. Cliquez sur Modifier, puis cliquez sur le bouton Workflow Studio sur le côté droit pour modifier la machine d'état dans Workflow Studio.

3. Commencez par supprimer les étapes **Update Order History**, **Update Data Warehouse**, **Update Customer Profile** et **Update Inventory** en cliquant sur chaque étape et en cliquant sur **Supprimer tous les états sélectionnés* *.

    ![Supprimer les étapes du *workflow* existantes](/static/img/module-13/delete-steps-from-workflow.png)

4. Maintenant, ajoutez une étape AWS Step Functions StartExecution, entre **Notify Payment Success** et **Ship the Package** en faisant glisser depuis la palette de gauche. Si StartExecution n'est pas disponible dans la section "Les plus populaires", tapez StartExecution dans la barre de recherche en haut de la palette.

    ![Ajouter l'étape StartExecution](/static/img/module-13/add-start-execution-step.png)

5. Cliquez sur l'étape **Step Functions StartExecution** que vous venez d'ajouter pour la configurer afin d'invoquer le workflow Express. Pour clarifier ce que fait ce *workflow* imbriqué, mettez à jour le "Nom de l'état" pour lire "Workflow to Update Backend Systems".

6. Ensuite, dans la zone "API Parameters", remplacez la valeur de l'attribut "StateMachineArn" par l'ARN que vous avez copié à l'étape 1. Cela indique à Step Functions quel workflow imbriqué a exécuter. Vous pouvez aussi éventuellement supprimer l'attribut "StatePayload", car il n'est pas utilisé par le workflow imbriqué.

    ![Configurer le Express workflow imbriqué](/static/img/module-13/configure-nested-express-workflow.png)

7. Une fois les mises à jour effectuées, cliquez sur le bouton **Appliquer et quitter**, puis sur le bouton **Enregistrer**.

8. Vous recevrez un avertissement indiquant que les modifications peuvent affecter les ressources auxquelles votre machine d'état doit accéder et, par conséquent, des mises à jour du rôle IAM utilisé par votre machine d'état peuvent être nécessaires. Pour plus de simplicité, le rôle contient déjà les autorisations requises, mais dans le monde réel, vous devez vous assurer de revoir le rôle IAM utilisé par votre machine d'état.

9. Exécutez la machine d'état mise à jour en cliquant sur le bouton **Démarrer l'exécution** dans le coin supérieur droit. La machine d'état ne nécessite aucune entrée - vous pouvez laisser l'attribut "Commentaire" qui est inclus par défaut, si vous le souhaitez. Cliquez sur **Démarrer l'exécution**. Vous pouvez maintenant regarder la machine d'état pendant que les étapes sont exécutées et vous devriez voir un diagramme entièrement vert. Maintenant, cliquez sur le lien "State Machines" sur le côté gauche et choisissez le flux de travail commençant par ChildStateMachine. Dans l'onglet "Surveillance", vous devriez voir une valeur de 1 pour la métrique "Exécutions démarrées" et une valeur de 1 pour la métrique "Exécutions réussies", indiquant que le workflow imbriqué a été exécuté avec succès.

    ![Statistiques d'exécution du workflow Child Express](/static/img/module-13/child-state-machine-execution-stats.png)
