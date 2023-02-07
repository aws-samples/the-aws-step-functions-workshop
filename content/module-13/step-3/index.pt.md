---
title: 'Visão geral da máquina de estados'
weight: 153

---
Na sua conta você possui uma máquina de estado com o nome começando com _ParentStateMachine_. A máquina de estado atual é um fluxo de trabalho Standard. Como mencionado no inicio desse módulo, isso pode ser necessário porque sua máquina de estados utilize funcionalidades disponíveis apenas para fluxos de trabalho Standard, como a funcionalidade .waitForTaskToken, ou porque a duração do fluxo de trabalho ultrapasse 5 minutos, ou porque você precise do modelo "execute apenas uma vez".  

Entretanto, repare na etapa destacado abaixo. Vamos assumir que as etapas abaixo são idempotentes e funcionariam bem no modelo de execução "pelo menos uma vez", como o fluxo de trabalho Express provém. Nós poderíamos mover essas etapas para um fluxo de trabalho Express aninhado.

![Steps that could move to an Express workflow](/static/img/module-13/state-machine-express-step-candidates.png)