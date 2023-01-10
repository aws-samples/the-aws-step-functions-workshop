---
title: 'Configurar o AWS Cloud9 Workspace'
weight: 133
---

- Faça login no AWS Console
- Navegue para o [AWS Cloud9](https://console.aws.amazon.com/cloud9/home) no console. Certifique-se de estar na região correta.
- Selecione **StepFunctionsSAMWorkshop** na lista de ambientes e clique no botão **Open in Cloud9** . Maximize a exibição do terminal fechando o **welcome tab** e a **lower work area**. Abra uma nova tab **terminal** na área de trabalho principal:
  ![AWS Cloud9 Antes](/static/img/setup/c9before.png)
- Seu ambiente de trabalho deve ter essa aparência:
  ![AWS Cloud9 Depois](/static/img/setup/c9after.png)

### Anexe uma função à instância do AWS Cloud9 EC2

- Na sua IDE do **AWS Cloud9** , clique em **Manage EC2 Instance** no menu to topo direito como mostra o diagrama a seguir.
  ![AWS Cloud9 manage](/static/img/setup/c9manageinstance.png)
- Selecione a instância AWS Cloud9 checando a caixa próxima a ela, então escolha **Actions / Security / Modify IAM Role**
  ![AWS Cloud9 instance role](/static/img/setup/c9instancerole.png)
- Escolha **stepfunctionsworkshop-sam-role** na caixa de seleção **IAM Role** , e selecione **Update IAM role**
- Retorne na sua área de trabalho e clique no sprocket, ou abra uma nova tab para abrir a tab de  Preferências
- Selecione **AWS Settings** na navegação esquerda.
- Deselecione **AWS managed temporary credentials**
- Feche a tab de Preferências
  ![AWS Cloud9 aws settings](/static/img/setup/c9disableiam.png)

Execute os seguintes comandos na janela de terminal.

Remova as credenciais existentes:

```bash
rm -vf ${HOME}/.aws/credentials
```
We 
Instale jq. Nós vamos usá-lo para ajudar no processamento json.

```bash
sudo yum install -y jq
```

Atualize o AWS CLI:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Configure o AWS CLI com a região atual como default:

```bash
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```

Verifique que AWS_REGION está setada corretamente:

```bash
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

Salve o AWS_ACCOUNT_ID e AWS_REGION no bash_profile:

```bash
echo "export AWS_ACCOUNT_ID=${AWS_ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

Verifique que a IDE do AWS Cloud9 está configurada para usar a IAM role:

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-sam-role -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

Caso a IAM role não seja válida, **DO NOT PROCEED**. Retorne e confirme os passos dessa página. E caso a IAM role seja válida clique **Next**.
