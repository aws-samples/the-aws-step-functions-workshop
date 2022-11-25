---
title: 'AWS CDK e Configuração do Projeto'
weight: 124
---

O ambiente AWS Cloud9 vem com alguns utilitários da AWS pré-instalados. Execute o comando a seguir em seu terminal AWS Cloud9 para verificar se ele contém uma versão atualizada do AWS CDK. Deve ser v2.x.

```bash
cdk --version
```

### Bootstrapping AWS CDK

A implantação de aplicativos do AWS CDK em um ambiente da AWS pode exigir que você provisione os recursos de que o AWS CDK precisa para realizar a implantação. Esses recursos incluem um bucket do Amazon S3 para armazenar arquivos e funções do IAM que concedem as permissões necessárias para realizar implantações. O processo de provisionamento desses recursos iniciais é chamado de bootstrapping. Isso normalmente precisa ser feito uma vez por região em uma determinada conta.

```bash
cdk bootstrap aws://${AWS_ACCOUNT_ID}/${AWS_REGION}
```

### Configure seu Projeto AWS CDK

Crie um novo diretório para o aplicativo AWS CDK e inicialize um projeto TypeScript.

```bash
mkdir stepfunctions-rest-api
cd stepfunctions-rest-api
cdk init --language typescript
```

::alert[Certifique-se de nomear o diretório `stepfunctions-rest-api`. O modelo de aplicativo AWS CDK usa o nome do diretório para gerar nomes para arquivos e classes de origem. Se você usar um nome diferente, seu aplicativo não corresponderá a este tutorial.]{header="Note"}

### Use o AWS CDK para criar uma API REST do API Gateway com integração de back-end Máquina de Estados Espresso Síncrona

Primeiro, revisaremos os trechos de código individuais que definem a Máquina de Estados Espresso Síncrona e a API REST do API Gateway. Mais tarde, vamos juntá-los em um aplicativo AWS CDK. Em seguida, sintetizaremos e implantaremos esses recursos.

#### Revise a definição de máquina de estado do Step Functions

Este código AWS CDK define uma máquina de estado simples com um estado `pass`. Revise este código agora.

```bash
const startState = new stepfunctions.Pass(this, 'PassState', {
    result: { value: 'Hello back to you!' },
})

const stateMachine = new stepfunctions.StateMachine(this, 'MyStateMachine', {
    definition: startState,
    stateMachineType: stepfunctions.StateMachineType.EXPRESS,
});
```

Observe que o trecho acima contém:

- Uma construção de estado `Pass` chamada `PassState`.
- Uma construção de Máquina de Estados chamada `MyStateMachine`.
    - A definição StateMachine especifica seu estado inicial.
    - O stateMachineType é `EXPRESS` (a construção `StepFunctionsRestApi` só permite uma máquina de estado Synchronous Express).

#### Revise a definição da API REST do API Gateway

Em seguida, usaremos a construção `StepFunctionsRestApi` para criar a API REST do API Gateway com as permissões necessárias e o mapeamento de entrada/saída padrão. Esta é uma construção de alto nível que contém muitas configurações predefinidas. Podemos usar essa definição para criar uma integração entre a máquina de estado e o API Gateway.

```bash
const api = new apigateway.StepFunctionsRestApi(this, 'StepFunctionsRestApi', { stateMachine: stateMachine });
```

#### Coloque tudo junto

No projeto AWS CDK, substitua o conteúdo do arquivo `lib/stepfunctions-rest-api-stack.ts` pelo código abaixo. Você reconhecerá as definições da máquina de estado do Step Functions e do API Gateway.

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

Substitua o conteúdo de `bin/stepfunctions-rest-api.ts` pelo código abaixo.

```bash
#!/usr/bin/env node
import 'source-map-support/register';
import * as cdk from 'aws-cdk-lib';
import { StepfunctionsRestApiStack } from '../lib/stepfunctions-rest-api-stack';

const app = new cdk.App();
new StepfunctionsRestApiStack(app, 'CDKStepfunctionsRestApiStack');
```

Salve esses arquivos de origem. Para implantar o Amazon API Gateway e a máquina de estado do AWS Step Functions em sua conta da AWS, execute o seguinte comando na raiz do aplicativo:
```bash
cdk deploy
```

Você será solicitado a aprovar as políticas do IAM que o AWS CDK gerou. Após concluir a implantação, o AWS CDK exibirá o URL da API REST como saída. Copie este URL. Você o usará para testar o aplicativo na próxima etapa.
