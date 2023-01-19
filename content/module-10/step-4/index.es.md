---
title: 'AWS CDK y configuración del proyecto'
weight: 124
---

El entorno AWS Cloud9 viene con algunas utilidades de AWS preinstaladas. Ejecute el siguiente comando en su terminal de AWS Cloud9 para verificar si contiene una versión actualizada de AWS CDK. Debería ser v2.x.

```bash
cdk --version
```

### Inicializando AWS CDK
Desplegar aplicaciones AWS CDK en un entorno de AWS puede requerir que provisione recursos que AWS CDK necesita para realizar el despliegue. Estos recursos incluyen un bucket de Amazon S3 para almacenar archivos y roles de IAM que otorgan los permisos necesarios para realizar despliegues. El proceso de provisionamiento de estos recursos iniciales se llama inicialización. Esto normalmente debe hacerse una vez por región en una cuenta dada.

```bash
cdk bootstrap aws://${AWS_ACCOUNT_ID}/${AWS_REGION}
```

### Configure su proyecto AWS CDK
Cree un nuevo directorio para la aplicación AWS CDK e inicialice un proyecto de TypeScript.

```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
cdk init --language typescript
```

::alert[Asegúrese de nombrar el directorio `stepfunctions-rest-api`. La plantilla de aplicación de AWS CDK utiliza el nombre del directorio para generar nombres de archivos y clases. Si utiliza un nombre diferente, su aplicación no coincidirá con este tutorial.]{header="Nota"}

### Utilice AWS CDK para crear una API Gateway REST API integrando de Máquina de Estado Express Síncrona

Primero, revisaremos los fragmentos de código individuales que definen la máquina de estado de Express síncrona y la API Gateway REST API. Luego, los combinaremos en una aplicación de AWS CDK. Luego, sintetizaremos y desplegaremos estos recursos.

### Revisar la definición de máquina de estado de Step Functions

Este código de AWS CDK define una máquina de estado simple con un estado `pass`. Revisa este código ahora.

```bash
const startState = new stepfunctions.Pass(this, 'PassState', {
    result: { value: 'Hello back to you!' },
})

const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
    definition: startState,
    stateMachineType: stepfunctions.StateMachineType.EXPRESS,
});
```

Fíjate en el fragmento anterior contiene:

- Un estado construct `Pass` llamado `PassState`.
- Un construct `StateMachine` llamado `MyStateMachine`.
  - La definición del StateMachine especifíca su estado inicial.
  - El tipo de stateMachine es `EXPRESS` (el construct `StepFunctionsRestApi` solo permite una máquina de estado sincrónica Express).

#### Revisa la definición de la API Gateway REST API

A continuación, revise el construct `StepFunctionsRestApi` a continuación. Este es un construct de alto nivel que contiene muchas configuraciones predefinidas. Utilizará este construct para crear la API REST en API Gateway con los permisos requeridos y el mapeo de entrada/salida predeterminado. También utilizará este construct para crear una integración entre la máquina de estado y API Gateway.

```bash
const api = new apigateway.StepFunctionsRestApi(this, 'StepFunctionsRestApi', { stateMachine: stateMachine });
```

#### Júntalo todo

En el proyecto de AWS CDK, reemplaza el contenido del archivo `lib/stepfunctions-rest-api-stack.ts` (bajo el directorio principal del proyecto) con el código de abajo. Reconocerás las definiciones de la máquina de estado de Step Functions y la API Gateway.

```bash
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

Reemplaza el contenido del archivo `bin/stepfunctions-rest-api.ts` (bajo el directorio principal del proyecto) con el siguiente código.

```bash
#!/usr/bin/env node
import 'source-map-support/register';
import * as cdk from 'aws-cdk-lib';
import { StepfunctionsRestApiStack } from '../lib/stepfunctions-rest-api-stack';

const app = new cdk.App();
new StepfunctionsRestApiStack(app, 'CDKStepfunctionsRestApiStack');
```

::alert[Cloud9 no guarda automáticamente tus archivos, así que asegúrate de guardarlos]{header="¡Guarda tus archivos!"}

Para desplegar Amazon API Gateway y la máquina de estado de AWS Step Functions en tu cuenta de AWS, ejecuta el siguiente comando desde la raíz de la aplicación:
```bash
cdk deploy
```

Se te pedirá que apruebes las políticas IAM que ha generado AWS CDK. Después de completar la implementación, AWS CDK mostrará la url de la API REST como salida. Copia esta url. La usarás para probar la aplicación en el siguiente paso.
