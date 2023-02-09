---
title: 'Substitua etapas por um fluxo de trabalho Express aninhado'
weight: 154

---

Vamos substituir as etapas no fluxo de trabalho Standard por um fluxo de trabalho Express aninhado. Um fluxo de trabalho Express aninhado com essas etapas já foram criados na sua conta com o nome começando em _ChildStateMachine_.

1. No [Console da Step Functions](https://console.aws.amazon.com/states/home), seleciona “State machines” no lado esquerdo e então clique na na máquina de estado com o nome começando em *ChildStateMachine*. Na caixa “Details” no alto, copie o valor do ARN, você irá precisar dele nas próximas etapas.  

2. Próximo, abra a máquina de estado com o nome começando em *ParentStateMachine*. Clique em Edit e depois no botão Workflow Studio do lado direito para editar a máquina de estado no Workflow Studio.   

3. Comece apagando as etapas **Update Order History**, **Update Data Warehouse**, **Update Customer Profile**, e **Update Inventory** selecionado-os e clicando em **Delete all selected states**.  

    ![Delete existing workflow steps](/static/img/module-13/delete-steps-from-workflow.png)

4. Agora, adicione uma etapa AWS Step Functions StartExecution, entre **Notify Payment Success** e **Ship the Package** arrastando ele da palheta do lado esquerdo. Se StartExecution não estiver disponível na seção “Most Popular”, digite StartExecution na barra de busca no topo da palheta. 

    ![Add StartExecution step](/static/img/module-13/add-start-execution-step.png)

5. Clique na etapa **Step Functions StartExecution** que você acabou de adicionar para configurá-lo e invocar o fluxo de trabalho Express. para ficar mais claro de como o fluxo de trabalho aninhado funciona, atualize o “State name” para “Workflow to Update Backend Systems.”  

6. Próximo, na caixa “API Parameters”, substitua o valor do atributo “StateMachineArn” pelo ARN que você copiou na etapa 1. Ele indica para a Step Functions qual fluxo de trabalho aninhado executar. Você também pode opcionalmente remover o atributo “StatePayload”, porque ele não será utilizado pelo fluxo de trabalho aninhado.  

    ![Configure nested Express workflow](/static/img/module-13/configure-nested-express-workflow.png)

7. Após efetuar as atualizações, clique no botão **Apply and Exit** e no botão **Save**.  

8. Você receberá um aviso alertando que as alterações poderão afetar quais recursos sua máquina de estado precisará acessar e por isso, atualizações na função IAM do seu fluxo de trabalho poderão ser necessárias. Para facilitar, a função IAM ja possui as permissões necessárias, mas na vida real, você deveria fazer a revisão da sua função IAM role usada pela máquina de estado.

9. Execute a máquina de estados atualizada clicando no botão **Start Execution** no canto direito superior. A máquina de estados não precisa de entrada de dados - caso queira, você pode deixar o atributo “Comment” com o valor padrão. Clique em **Start Execution**. Você pode assistir a máquina de estados a medida em que as etapas são executados e ao final ver o diagrama todo verde. Agora, clique no link “State Machines” no lado esquerdo e escolha o fluxo de trabalho com _ChildStateMachine_. Na aba “Monitoring”, você deverá ver o valor 1 para a métrica “Executions Started”, e o valor 1 para a métrica “Executions Succeeded”, indicando que o fluxo de trabalho aninhado foi executado com sucesso.

    ![Child Express workflow execution stats](/static/img/module-13/child-state-machine-execution-stats.png)

::alert[**Parabéns!** Você substituiu várias etapas de um fluxo de trabalho Standard por um fluxo de trabalho Express aninhado!]{type="success"}
