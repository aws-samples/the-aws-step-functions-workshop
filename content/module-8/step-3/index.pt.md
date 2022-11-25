---
title: 'Tratando falha usando Retry'
weight: 103
---

Estados `Task` e `Parallel` podem ter um campo chamado `Retry`, com uma lista de objetos conhecidos como retriers. Um retrier individual representa um certo número de retries, normalmente aumentando os intervalos de tempo.

No exercício abaixo você criará uma definição de ASL que invocará uma função Lambda. A função Lambda foi criada para falhar. você implementará um `Retry` para esta função, configurando o máximo de tentativas com uma taxa de recuo exponencial entre retries.

1. Encontre a [função Lambda](https://console.aws.amazon.com/lambda/home) **ErrorHandlingCustomErrorFunction**. Copie o ARN da função e revise o código. Repare que a função está preparada para lançar um erro.

   ![Lambda function throws FooError](/static/img/module-8/error-handling-lambda-foo-error.png)

2. Encontre a [máquina de estado](https://console.aws.amazon.com/states/home) **ErrorHandlingStateMachineWithRetry-...**. Clique no seu link e depois clique no botão **Edit** no canto direito superior da tela. 

3. No campo `Resource`, Substitua o valor atual pelo ARN da função Lambda copiado no passo 1. Quando a máquia de estados incovar essa função Lambda, ela irá falhar. Você pode reiniciar a execução para ver a falha.

   ![Replace Lambda function ARN](/static/img/module-8/error-handling-state-machine-retry.png)


4. Agora implemente um `Retry`. Copie o código exibido abaixo e cole começando na linha 8 entre os nós `Resource` e `End`. 

```bash
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
```

5. Revise os parâmetros de tratamento de erro. Esses parâmetros definem o comportamento do `Retry`.

- ErrorEquals (Obrigatório)

  > Uma lista não vazia com os nomes dos erros. Quando um estado reporta um erro a Step Function o procura nos retriers. Quando o nome do erro aparece na lista ela implementa a política de retry definida no retrier.

- IntervalSeconds (Opcional)

  > Um número inteiro que representa a quantidade de segundos que devem ser aguardados antes do retry (1 é o padrão). IntervalSeconds tem o valor máximo de 99999999.

- MaxAttempts (Opcional)

  > Um número inteiro que representa a quantidade máxima de retries (3 é o padrão). Se o número máximo de retries for excedido a execução é finalizada com tratamento de erro normal. O valor zero deve ser usado quando não se deve fazer nenhum retry. MaxAttempts tem o valor máximo de 99999999.

- BackoffRate (Opcional)

  > O multiplicador pelo qual o intervalo entre retries deve ser acrescido (2.0 é o padrão).

Revise a documentação para mais informações sobre [parâmetros de tramento de erros](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-error-handling.html).


6. Clique em **Save** e depois em **Start execution**. Aceite a entrada padrão e clique em **Start execution** novamente.

7. Para ver a mensagem de erro customizada, selecione `StartExecution` no gáfico do painel de inspeção e clique na aba **Exception**.
   ![Failure using Retry output](/static/img/module-8/error-handling-custom-error-retry-output.png)

8. Revise o **Execution event history** para ter mais detalhes sobre a execução. Veja as retentativas na execução.
   ![Failure using Retry event history](/static/img/module-8/error-handling-custom-error-retry-event-history.png)

### Tendo problemas?

Sua definição de ASL deve ser similar ao trecho de código abaixo. Lembre-se de substituir o ARN da função Lambda no nó `Resource`.

```bash
{
  "Comment": "A state machine calling an AWS Lambda function with Retry",
  "StartAt": "StartExecution",
  "States": {
    "StartExecution": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:FailFunction",
      "Retry": [
        {
          "ErrorEquals": [
            "CustomError"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "End": true
    }
  }
}
```
Quando você tiver concluído, poderá avançar para próxima página.
