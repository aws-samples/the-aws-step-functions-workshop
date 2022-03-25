---
title: 'Cloud9 Workspace Setup'
weight: 111
---

### Launch Cloud9 in your closest region

:::alert{header="Important" type="warning"}
Follow the instructions on this page only if you are executing this workshop in your own account. To skip these instructions [click here](../step-2).
:::

- Log into the AWS Console
- Select Cloud9 from list of services. Make sure you have chosen the region in which you want to configure your environment
- Select **Create environment**
- Name it **stepfunctionsworkshop**, and select **Next Step**
- Change the Instance type to **t3.small**, and select **Next Step**
- Lastly, select **Create Environment**
- When it comes up, customize the environment by closing the **welcome tab** and **lower work area**, and opening a new **terminal** tab in the main work area:
  ![Cloud9 Before](/static/img/setup/c9before.png)
- Your workspace should now look like this:
  ![Cloud9 After](/static/img/setup/c9after.png)
- If you like this theme, you can choose it yourself by selecting View / Themes / Solarized / Solarized Dark in the Cloud9 workspace menu.

### Create the IAM Role

:::alert{header="Important" type="warning"}
Follow the instructions in this section only if you are trying this in your own account.
:::

- Navigate to IAM section of the AWS console. Click on **Roles** in the left hand menu and then select **Create Role**
- Confirm that **AWS service** and **EC2** are selected, then click **Next** to view permissions.
- Confirm that **AdministratorAccess** is checked, then click **Next: Tags** to assign tags.
- Enter **stepfunctionsworkshop-admin** for the Name, and click **Create role**.

### Attach the role to the EC2 instance

- Navigate back to your **cloud9** instance and click on **Manage EC2 Instance** from the top right menu as shown in the diagram below
  ![Cloud9 manage](/static/img/setup/c9manageinstance.png)
- Select the instance, then choose **Actions / Security / Modify IAM Role**
  ![Cloud9 instance role](/static/img/setup/c9instancerole.png)
- Choose **stepfunctionsworkshop-admin** from the **IAM Role** drop down, and select **Apply**
- Return to your workspace and click the sprocket, or launch a new tab to open the Preferences tab
- Select **AWS SETTINGS**
- Turn off **AWS managed temporary credentials**
- Close the Preferences tab
  ![Cloud9 aws settings](/static/img/setup/c9disableiam.png)

To ensure temporary credentials aren’t already in place we will also remove any existing credentials file:

```bash
rm -vf ${HOME}/.aws/credentials
```

Install jq, as we will use this quite a bit throughout the workshop when interacting with json outputs.

```bash
sudo yum install -y jq
```

Upgrade AWS CLI according to guidance in AWS documentation.

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

We should configure our aws cli with our current region as default.

```bash
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```

Check if AWS_REGION is set to desired region

```bash
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

Let’s save these into bash_profile

```bash
echo "export AWS_ACCOUNT_ID=${AWS_ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

Validate the IAM role
Use the **GetCallerIdentity** CLI command to validate that the Cloud9 IDE is using the correct IAM role.

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-admin -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

If the IAM role is not valid, **DO NOT PROCEED**. Go back and confirm the steps on this page.

### Increase the disk size on the Cloud9 instance

```bash
pip3 install --user --upgrade boto3
export instance_id=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
python3 -c "import boto3
import os
from botocore.exceptions import ClientError
ec2 = boto3.client('ec2')
volume_info = ec2.describe_volumes(
    Filters=[
        {
            'Name': 'attachment.instance-id',
            'Values': [
                os.getenv('instance_id')
            ]
        }
    ]
)
volume_id = volume_info['Volumes'][0]['VolumeId']
try:
    resize = ec2.modify_volume(
            VolumeId=volume_id,
            Size=30
    )
    print(resize)
except ClientError as e:
    if e.response['Error']['Code'] == 'InvalidParameterValue':
        print('ERROR MESSAGE: {}'.format(e))"
if [ $? -eq 0 ]; then
    sudo reboot
fi
```

_Note_: The above command is adding more disk space to the root volume of the EC2 instance that Cloud9 runs on. Once the command completes, we reboot the instance which could take a minute or two for the IDE to come back online.
