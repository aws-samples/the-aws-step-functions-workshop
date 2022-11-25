---
title: 'Tratando falhas usando Catch'
weight: 103
---

Estados `Task`, `Map` e `Parallel` podem conter campos chamados `Catch`. O valor desse campos deve ser uma lista de objetos, conhecidos como catchers. Cada catcher pode ser considerado para pegar um determinado tipo de erro. ASL define um conjunto de palavras para os nomes de erros mais conhecidos, todos começando com o prefixo `States.`. Catchers também podem pegar erros customizados. Cada catcher pode ser configurado para encaminhar o erro para um estado **fallback**. Cada estado fallback pode implementar uma lógica de tratamento de erros. Tipos de erros nativos incluem:

- `States.ALL` - um tipo de erro para pegar qualquer erro
- `States.DataLimitExceeded` - erro de cota excedida
- `States.Runtime` - exceção de tempo de execução que não pôde ser tratada
- `States.HeartbeatTimeout` - um estado Task não conseguiu enviar o sinal de vida
- `States.Timeout` - um estado task excedeu limite de tempo
- `States.TaskFailed` - um estado Task falhou na sua execução
- `States.Permissions` - um estado task não tem permissões suficientes

Quando um estado tem ambos campos Retry e Catch, a Step Functions usa o apropriado retry primeiro e aplica a transição para catch somenbte se a política de retry falhar em tratar o erro.

Leia a documentação para mais informações em [nomes de Erros](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html).

Neste exercício, você irá configurar a máquina de estado para pegar um erro customizado e usar o erro `States.Timeout` no campo `Catch`. 

### Pegando um erro customizado

1. Encontre a [função Lambda](https://console.aws.amazon.com/lambda/home) **ErrorHandlingCustomErrorFunction**. Copie o ARN da função e revise o código. Veja que o código lança um erro chamado `CustomError`.

   ![Lambda function throws CustomError](/static/img/module-8/error-handling-lambda-function-custom-error.png)

2. Agora localize a [máquina de estado](https://console.aws.amazon.com/states/home) **ErrorHandlingStateMachineWithCatch-...** . Clique no seu link e depois clique no botão **Edit** no canto superior direito da tela. 

3. No campo `Resource`, substitua o valor atual pelo ARN da função Lambda copiado no passo 1. Quando a máquina de estados invocar a função Lambda, a função irá falhar com o erro `CustomError`.

   ![Replace Lambda function ARN](/static/img/module-8/error-handling-state-machine-catch.png)

4. Revise o bloco `Catch` da sua definiçao ASL. Veja que ela possui três catchers. O primeiro catcher para pegar o erro chamado `CustomError`.Quando ele pega esse erro, passo o fluxo para o estado fallback `CustomErrorFallback`.

   ![Catch CustomError](/static/img/module-8/error-handling-state-machine-catch-custom-error.png)

5. Clique em **Save** e então em **Start execution**. Aceite o valor de entrada padrão e clique em **Start execution** novamente.

6. Vá para aba **Execution output** a saída do seu fluxo de trabalho. Ele deveria exibir `This is a fallback from a custom Lambda function exception`

7. Para ver a saída do estado fallback, selecione o estado `CustomErrorFallback` no gráfico do painel de inspeção e clique na aba **Step output**.
   ![Saída do Catch](/static/img/module-8/error-handling-custom-error-catch-output.png)
8. Percorra através de **Execution event history** para ver mais detalhes.
   ![Histórico de eventos do Catch](/static/img/module-8/error-handling-custom-error-catch-event-history.png)



### Pegue um erro de timeout

1. Localize a [Lambda function](https://console.aws.amazon.com/lambda/home) **ErrorHandlingSleep10Function**. Copie o ARN da função Lambda e revise o código. Veja que a função está configurada para dar uma pausa de 10 segundos na execuçao.

   ![Pausa de 10 segundos na execução da Lambda function](/static/img/module-8/error-handling-lambda-sleep10.png)

2. Agora localize a [máquina de estado](https://console.aws.amazon.com/states/home) **ErrorHandlingStateMachineWithCatch-...**. Clique no seu link e depois clique no botão **Edit** no canto superior direito da tela. 

3. No campo `Resource`, substitua o valor atual pelo ARN da função lambda copiado no passo 1. Quando a máquina de estados invocar essa função ela irá pausar a execução por 10 segundos.

   ![Substitua o ARN da função Lambda](/static/img/module-8/error-handling-state-machine-catch.png)

4. Veja que o campo `TimeoutSeconds` da `Task` está configurado para 5 segundos.Veja que o catcher está configurado para pegar o tipo de erro `States.Timeout`. Esse catcher encaminha para o estado `TimeoutFallback`. 

   ![Revise o Timeout Catcher](/static/img/module-8/error-handling-state-machine-timeout.png)

5. Clique em **Save** e depois em **Start execution**. Aceite o valor padrão e clique em **Start execution** novamente.

6. Vá para aba **Execution output** e veja a saída do seu fluxo de trabalho. Ele deveria exibir `This is a fallback from a timeout Lambda function exception`

7. Para ver a saída do estado fallback, selecione o estado `TimeoutFallback` no gráfico no painel de inspeção e clique na aba **Step output**.
   ![Saída do Catch](/static/img/module-8/error-handling-timeout-error-catch-output.png)

8. Percorra através de **Execution event history** para ver mais detalhes
   ![Histórico de eventos do Catch](/static/img/module-8/error-handling-timeout-error-catch-event-history.png)

   ::alert[Parabéns! Você completou o módulo de tratamento de erros com sucesso.]{type="success"}
