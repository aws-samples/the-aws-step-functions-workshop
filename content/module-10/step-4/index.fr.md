---
title: 'AWS CDK et mise en place du projet'
weight: 124
---

L'environnement AWS Cloud9 est fourni avec certains utilitaires AWS préinstallés. Exécutez la commande suivante dans votre terminal AWS Cloud9 pour vérifier qu'il contient une version mise à jour d'AWS CDK. Il devrait être v2.x.

```bash
cdk --version
```

### Amorçage d'AWS CDK

Le déploiement d'applications AWS CDK dans un environnement AWS peut nécessiter que vous provisionniez les ressources dont AWS CDK a besoin pour effectuer le déploiement. Ces ressources incluent un bucket Amazon S3 pour le stockage des fichiers et des rôles IAM qui accordent les autorisations nécessaires pour effectuer les déploiements. Le processus de provisionnement de ces ressources initiales est appelé amorçage. Cela doit généralement être fait une fois par région dans un compte donné.

```bash
cdk bootstrap aws://${AWS_ACCOUNT_ID}/${AWS_REGION}
```

### Configurer votre projet AWS CDK

Créez un nouveau répertoire pour l'application AWS CDK et initialisez un projet TypeScript.

```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
cdk init --language typescript
```

::alert[Assurez-vous de nommer le répertoire `stepfunctions-rest-api`. Le modèle d'application AWS CDK utilise le nom du répertoire pour générer des noms pour les fichiers source et les classes. Si vous utilisez un nom différent, votre application ne correspondra pas à ce didacticiel.]{header="Note"}

### Utiliser AWS CDK pour créer une REST API Gateway avec integration à Synchronous Express State Machine

Tout d'abord, nous allons examiner les extraits de code individuels qui définissent la machine à états Synchronous Express et l'API REST API Gateway. Plus tard, nous les rassemblerons dans une application AWS CDK. Ensuite, nous synthétiserons et déploierons ces ressources.

#### Passer en revue la définition de la machine à états Step Functions

Ce code AWS CDK définit une machine à états simple avec un état `pass`. Passez ce code en revue.

```typescript
const startState = new stepfunctions.Pass(this, 'PassState', {
    result: { value: 'Hello back to you!' },
})

const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
    definition: startState,
    stateMachineType: stepfunctions.StateMachineType.EXPRESS,
});
```
Notez que l'extrait ci-dessus contient :

- Un contruct pour l'état `Pass` nommé `PassState`.
- Un contruct pour la StateMachine nommé `MyStateMachine`.
  - La définition StateMachine spécifie son état de départ.
  - Le stateMachineType est `EXPRESS` (le construct `StepFunctionsRestApi` n'autorise qu'une machine à états Synchronous Express).

#### Examiner la définition de l'API REST API Gateway

Passez ensuite en revue le construct `StepFunctionsRestApi` ci-dessous. Il s'agit d'un construct de haut niveau qui contient de nombreuses configurations prédéfinies. Vous utiliserez cette construction pour créer l'API REST API Gateway avec les autorisations requises et le mappage d'entrée/sortie par défaut. Vous utiliserez également cette construction pour créer une intégration entre la machine à états et API Gateway.

```typescript
const api = new apigateway.StepFunctionsRestApi(this, 'StepFunctionsRestApi', { stateMachine: stateMachine });
```

#### Assemblage

Dans le projet AWS CDK, remplacez le contenu du fichier `lib/stepfunctions-rest-api-stack.ts` (sous le répertoire principal du projet) par le code ci-dessous. Vous reconnaîtrez les définitions de la machine à états Step Functions et de l'API Gateway.

```typescript
import * as cdk from 'aws-cdk-lib';
import * as stepfunctions from 'aws-cdk-lib/aws-stepfunctions';
import * as apigateway from 'aws-cdk-lib/aws-apigateway';

export class StepfunctionsRestApiStack extends cdk.Stack {
    constructor(app: cdk.App, id: string) {
      super(app, id);

      const startState = new stepfunctions.Pass(this, 'PassState', {
          result: { value:'Hello back to you!' },
      })

      const stateMachine = new stepfunctions.StateMachine(this, 'CDKStateMachine', {
          definition: startState,
          stateMachineType: stepfunctions.StateMachineType.EXPRESS,
      });

      const api = new apigateway.StepFunctionsRestApi(this, 'CDKStepFunctionsRestApi', { stateMachine: stateMachine });
    }
}
```

Remplacez le contenu de `bin/stepfunctions-rest-api.ts` (sous le répertoire principal du projet) par le code ci-dessous.

```typescript
#!/usr/bin/env node
import 'source-map-support/register';
import * as cdk from 'aws-cdk-lib';
import { StepfunctionsRestApiStack } from '../lib/stepfunctions-rest-api-stack';

const app = new cdk.App();
new StepfunctionsRestApiStack(app, 'CDKStepfunctionsRestApiStack');
```

::alert[Cloud9 n'enregistre pas automatiquement vos fichiers, alors assurez-vous de les enregistrer]{header="Enregistrez vos fichiers !"}

Pour déployer Amazon API Gateway et la machine à états AWS Step Functions sur votre compte AWS, exécutez la commande suivante à partir de la racine de l'application :

```bash
cdk deploy
```

Vous serez invité à approuver les stratégies IAM générées par AWS CDK. Une fois le déploiement terminé, AWS CDK affichera l'URL de l'API REST en sortie. Copiez cette URL. Vous l'utiliserez pour tester l'application à l'étape suivante.
