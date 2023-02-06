---
title: 'Module 9 - Intégrations de services avec le SDK AWS'
weight: 110
---

AWS Step Functions s'intègre à de nombreux autres services AWS. Vous pouvez utiliser Step Functions [AWS SDK service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/supported-services-awssdk.html) pour appeler plus de 220 services AWS directement depuis votre machine à étatss, vous donnant accès à plus de 10 000 actions API.

Pour utiliser les intégrations AWS SDK, vous spécifiez le nom du service et l'appel d'API. Certaines intégrations nécessitent des paramètres et vous pouvez éventuellement spécifier un modèle d'intégration de service. Notez que l'action de l'API sera en casse camel et que les noms de paramètres seront en casse Pascal. Vous pouvez utiliser Amazon States Language pour spécifier une action d'API AWS dans le champ Resource d'un état de tâche. Pour ce faire, utilisez la syntaxe suivante :

`arn:aws:states:::aws-sdk:serviceName:apiAction.[serviceIntegrationPattern]`

**Exemples**

- Pour décrire les instances Amazon EC2, utilisez la syntaxe : `arn:aws:states:::aws-sdk:ec2:describeInstances`. Cela renverra en sortie la valeur de retour de l'appel d'API `describeInstances` d'Amazon EC2.

- Pour répertorier les compartiments dans Amazon S3, utilisez `arn:aws:states:::aws-sdk:s3:listBuckets`. Cela renverra en sortie la valeur de retour de l'appel d'API Amazon S3 `listBuckets`.

- Pour démarrer une exécution imbriquée dans Step Functions, utilisez la syntaxe : `arn:aws:states:::aws-sdk:sfn:startExecution`. Vous ajouterez ensuite `StateMachineArn` en tant que paramètre. Cela renverra en sortie la valeur de retour du workflow imbriqué Step Functions.

**Durée estimée : 10 minutes**