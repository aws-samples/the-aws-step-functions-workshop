---
title: 'Registre o histórico de execução com os Logs do Amazon CloudWatch'
weight: 144
---

Os fluxos de trabalho padrão registram o histórico de execução no AWS Step Functions, embora você possa, opcionalmente, configurar o registro no Amazon CloudWatch Logs. Ao criar um fluxo de trabalho padrão, ele não será configurado para habilitar o log no CloudWatch Logs por padrão. Para configurar o log, você pode passar o parâmetro LoggingConfiguration ao usar CreateStateMachine ou UpdateStateMachine. O CloudWatch Logs oferece várias vantagens para a análise de arquivos de log em relação ao log padrão, incluindo a capacidade de analisar melhor seus dados usando o CloudWatch Logs Insights. Para mais informações, veja [Analyzing Log Data with CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html). Para entender as políticas de IAM necessárias para registro no CloudWatch Logs, leia[IAM Policies for logging to CloudWatch Logs](https://docs.aws.amazon.com/step-functions/latest/dg/cw-logs.html#cloudwatch-iam-policy).

## Configure os Logs do CloudWatch

1. Abra o [Step Functions Console](https://console.aws.amazon.com/states/home) em seu console da AWS. Verifique se você está na região correta.

2. Clique em **State machines** na navegação à esquerda. Você verá a máquina de estado denominada DetectSentimentStateMachine-XXXX implantada para você como parte deste laboratório.

3. Clique na máquina de estados **DetectSentimentStateMachine-XXXX** .

4. Na página DetectSentimentStateMachine, clique na guia **Logging**. Você verá que o nível de log está desativado, o que indica que o log do CloudWatch não está ativado.

   ![CW Log disabled](/static/img/module-12/cw-log-disabled.png)

    Vamos habilitar o log do CloudWatch.

5. Clique em **Editar** no topo da página.

6. Na página Edit DetectSentimentStateMachine, role para baixo para alterar o nível de log em Logging para **ALL** e deixe o restante como padrão.

   ![CW Log enabled](/static/img/module-12/cw-logging-enabled.png)

7. Clique **Save** no topo da página.

8. Na caixa de diálogo da função do IAM, clique em **Salvar mesmo assim**.

Volte para a página DetectSentimentStateMachine e aguarde alguns minutos. Atualize a página e você verá a seção CloudWatch Logs Insights preenchida com logs.

   ![CW Logs](/static/img/module-12/cw-logs.png)

## Consultar insights de logs do CloudWatch

1. Abra o [CloudWatch console](https://console.aws.amazon.com/cloudwatch/home). Clique em **Logs Insights** em Logs no menu de navegação à esquerda.

2. Na página Logs Insights, selecione **/aws/vendedlogs/states/DetectSentimentStateMachine-XXX-Logs** grupo de logs.

   ![CWL Vended](/static/img/module-12/cwl-vendedlogs.png)

3. No campo de texto, copie e cole a consulta a seguir e clique em **Executar consulta**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, type
| stats count(*) as typeCount by type 
| sort typeCount desc
:::

   Esta consulta do CloudWatch Log Insights exibe as estatísticas de vários tipos de execução.

   ![CWL query](/static/img/module-12/cwl-query.png)

   Papel para baixo na seção de resultados para revisar os resultados completos. Você verá os resultados TaskFailed e ExecutionFailed.

   ![CWL failed](/static/img/module-12/cwl-failed.png)

   12. Para identificar a causa das execuções com falha, copie e cole a seguinte consulta no campo de texto do CloudWatch Log Insights e clique em **Run query**.

:::code{showCopyAction=true showLineNumbers=false}
fields @timestamp, execution_arn, details.error, details.cause
| filter type = 'TaskFailed'
| limit 100
:::

![CWL failureReasons 1](/static/img/module-12/cwl-failureReasons-1.png)

![CWL CWL failureReasons 2](/static/img/module-12/cwl-failureReasons-2.png)

Esses erros indicam que as falhas de execução do Step Functions ocorreram devido à limitação da taxa de transferência provisionada do DynamoDB. No próximo módulo, você usará o rastreamento de raios-X para investigar melhor essas falhas.
