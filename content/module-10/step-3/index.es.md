---
title: 'Configuración de espacio de trabajo de AWS Cloud9'
weight: 123
---

- Inicia sesión en la consola de AWS
- Navega a [AWS Cloud9](https://console.aws.amazon.com/cloud9/home) en la consola. Asegúrate de estar en la región correcta.
- Selecciona **StepFunctionsCDKWorkshop** de la lista de entornos y haz clic en **Open in Cloud9**. Maximiza la pantalla de terminal cerrando la pestaña **Welcome** y el **área de trabajo inferior**. Abre una nueva pestaña de **terminal** en el área de trabajo principal:
  ![AWS Cloud9 Before](/static/img/setup/c9before.png)
- Tu espacio de trabajo debería verse así:
  ![AWS Cloud9 After](/static/img/setup/c9after.png)

### Adjuntar un rol a la instancia EC2 de AWS Cloud9

- Desde tu IDE **AWS Cloud9**, haz clic en **Manage EC2 instance** en el menú de la parte superior derecha como se muestra en el diagrama a continuación.
  ![AWS Cloud9 manage](/static/img/setup/c9manageinstance.png)
- Selecciona la instancia de AWS Cloud9 marcando la casilla junto a ella, luego elige **Acciones / Seguridad / Modificar rol de IAM**
  ![AWS Cloud9 instance role](/static/img/setup/c9instancerole.png)
- Elige **stepfunctionsworkshop-cdk-role** desde el menú desplegable **Role de IAM**, y selecciona **Actualizar rol de IAM**
- Regresa a tu espacio de trabajo y ve a Preferencias
- Selecciona **AWS Settings** en la navegación izquierda.
- Desactiva **AWS managed temporary credentials**
- Cierra la pestaña Preferencias
  ![AWS Cloud9 aws settings](/static/img/setup/c9disableiam.png)

Ejecuta los siguientes comandos en la ventana de terminal.

Elimina cualquier credencial existente:

```bash
rm -vf ${HOME}/.aws/credentials
```

Instala `jq`. Lo usaremos para ayudarnos a procesar json.

```bash
sudo yum install -y jq
```

Actualiza AWS CLI:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Configura el AWS CLI con la región actual como predeterminada:

```bash
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```

Verifica que AWS_REGION esté como variable de entorno correctamente:

```bash
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

Salva AWS_ACCOUNT_ID y AWS_REGION en tu bash_profile:

```bash
echo "export AWS_ACCOUNT_ID=${AWS_ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

Verifica que el AWS Cloud9 IDE está configurado para usar el rol de IAM apropiado:

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-cdk-role -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

Si el rol de IAM no es válido, **NO CONTINÚES**. Regresa y revisa los pasos de esta página nuevamente. Si el rol es válido, haz clic en **Next**.
