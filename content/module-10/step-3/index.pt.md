---
title: 'Configuração do Workspace no AWS Cloud9'
weight: 123
---

- Faça login no Console AWS
- Navegue até [AWS Cloud9](https://console.aws.amazon.com/cloud9/home) no console. Verifique se você está na região correta.
- Selecione **StepFunctionsWorkshop** na lista de ambientes e clique no botão **Open in Cloud9**. Maximize a exibição do terminal fechando a **welcome tab** e a **lower work area**. Abra uma nova guia **terminal** na área de trabalho principal:
  ![AWS Cloud9 Antes](/static/img/setup/c9before.png)
- Seu espaço de trabalho agora deve ficar assim:
  ![AWS Cloud9 Depois](/static/img/setup/c9after.png)

### Anexar uma role à instância do AWS Cloud9 EC2

- Na IDE do **AWS Cloud9**, clique em **Manage EC2 Instance** no menu superior direito, conforme mostrado no diagrama abaixo.
  ![AWS Cloud9 manage](/static/img/setup/c9manageinstance.png)
- Selecione a instância do AWS Cloud9 marcando a caixa ao lado dela e escolha **Ações / Segurança / Modificar função do IAM**.
  ![Função da instância do AWS Cloud9](/static/img/setup/c9instancerole.png)
- Escolha **stepfunctionsworkshop-cdk-role** na lista suspensa **Função do IAM** e selecione **Atualizar função do IAM**
- Retorne ao seu espaço de trabalho e clique na roda dentada ou inicie uma nova guia para abrir a guia Preferências
- Selecione **AWS Settings** na navegação à esquerda.
- Desative as **AWS managed temporary credentials**
- Feche a guia Preferências
  ![Configurações do AWS Cloud9 aws](/static/img/setup/c9disableiam.png)

Execute os comandos a seguir na janela do terminal.

Remova quaisquer credenciais existentes:

```bash
rm -vf ${HOME}/.aws/credentials
```

Instale o jq. Usaremos isso para nos ajudar a processar o json.

```bash
sudo yum install -y jq
```

Upgrade AWS CLI:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Configure a AWS CLI com a região atual como padrão:

```bash
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```

Verifique se AWS_REGION está definido corretamente:

```bash
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

Salve AWS_ACCOUNT_ID e AWS_REGION no bash_profile:

```bash
echo "export AWS_ACCOUNT_ID=${AWS_ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

Verifique se o AWS Cloud9 IDE está configurado para usar a função correta do IAM:

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-cdk-role -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

Se a função do IAM não for válida, **NÃO CONTINUE**. Volte e confirme as etapas nesta página. Se a função for válida, clique em **Next**.
