---
title: "Configuration de l'espace de travail AWS Cloud9"
weight: 133
---

- Connectez-vous à la console AWS
- Accédez à [AWS Cloud9](https://console.aws.amazon.com/cloud9/home) dans la console. Assurez-vous d'être dans la bonne région.
- Sélectionnez **StepFunctionsWorkshop** dans la liste des environnements et cliquez sur le bouton **Open in Cloud9**. Maximisez l'affichage du terminal en fermant l'onglet **Welcome** et la **zone de travail inférieure**. Ouvrez un nouvel onglet **terminal** dans la zone de travail principale :
  ![AWS Cloud9 avant](/static/img/setup/c9before.png)
- Votre espace de travail devrait maintenant ressembler à ceci:
  ![AWS Cloud9 après](/static/img/setup/c9after.png)

### Attacher un rôle à l'instance AWS Cloud9 EC2

- Dans votre IDE **AWS Cloud9**, cliquez sur **Manage EC2 instance** dans le menu en haut à droite, comme indiqué dans le schéma ci-dessous.
  ![AWS Cloud9 gestion](/static/img/setup/c9manageinstance.png)
- Sélectionnez l'instance AWS Cloud9 en cochant la case à côté, puis choisissez **Actions / Sécurité / Modifier le rôle IAM**
  ![Rôle de l'instance AWS Cloud9](/static/img-fr/setup/c9instancerole.png)
- Choisissez **stepfunctionsworkshop-sam-role** dans le menu déroulant **Rôle IAM**, puis sélectionnez **Mettre â jours le rôle IAM**
- Revenez à votre espace de travail et cliquez sur le pignon, ou lancez un nouvel onglet pour ouvrir l'onglet Préférences
- Sélectionnez **AWS Settings** dans la navigation de gauche.
- Désactiver les **AWS managed temporary credentials**
- Fermez l'onglet Préférences
  ![Paramètres AWS Cloud9](/static/img/setup/c9disableiam.png)

Supprimez tous les identifiants existants :

```bash
rm -vf ${HOME}/.aws/credentials
```

Installez jq. Nous allons l'utiliser pour nous aider à traiter des données au format json.

```bash
sudo yum install -y jq
```

Mettez à jours l'AWS CLI :

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Configurez l'AWS CLI avec la région actuelle par défaut :

```bash
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```

Vérifiez que AWS_REGION est correctement défini :

```bash
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```
Enregistrez AWS_ACCOUNT_ID et AWS_REGION dans `.bash_profile` :

```bash
echo "export AWS_ACCOUNT_ID=${AWS_ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

Vérifiez que l'AWS Cloud9 IDE est configuré pour utiliser le bon rôle IAM :

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-sam-role -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

Si le rôle IAM n'est pas valide, **NE CONTINUEZ PAS**. Revenez en arrière et confirmez les étapes sur cette page. Si le rôle est valide, cliquez sur **Next**.
