---
title: 'Cloud9 Workspace Setup'
weight: 111
---

### Launch Cloud9

:::alert{header="Important" type="warning"}
Follow the instructions on this page only if you are executing this workshop in your own account. To skip these instructions [click here](../step-2).
:::

- Log into the AWS Console
- Select Cloud9 from list of services. Make sure you have chosen the region in which you want to configure your environment
- Select **Create environment**
- Name it **stepfunctionsworkshop**, and select **Next Step**
- Change the Instance type to **t3.small**, and select **Next Step**
- Select **Create Environment**
- When the environment completes, customize the display by closing the **welcome tab** and the **lower work area**. Open a new **terminal** tab in the main work area:
  ![Cloud9 Before](/static/img/setup/c9before.png)
- Your workspace should now look like this:
  ![Cloud9 After](/static/img/setup/c9after.png)

### Create an IAM Role

:::alert{header="Important" type="warning"}
Follow the instructions in this section only if you are trying this in your own account.
:::

- In a new tab, navigate to IAM section of the AWS console. Click on **Roles** in the left hand menu and then select **Create Role**
- Confirm that **AWS service** and **EC2** are selected, then click **Next** to view permissions.
- Attach the **AdministratorAccess** policy to the role, then click **Next: Tags** to assign tags.
- Enter **stepfunctionsworkshop-role** for the Name, and click **Create role**.

### Attach the role to the EC2 instance

- Navigate back to your **cloud9** instance and click on **Manage EC2 Instance** from the top right menu as shown in the diagram below
  ![Cloud9 manage](/static/img/setup/c9manageinstance.png)
- Select the cloud9 instance by checking the box next to it, then choose **Actions / Security / Modify IAM Role**
  ![Cloud9 instance role](/static/img/setup/c9instancerole.png)
- Choose **stepfunctionsworkshop-role** from the **IAM Role** drop down, and select **Save**
- Return to your workspace and click the sprocket, or launch a new tab to open the Preferences tab
- Select **AWS SETTINGS**
- Turn off **AWS managed temporary credentials**
- Close the Preferences tab
  ![Cloud9 aws settings](/static/img/setup/c9disableiam.png)

Remove any existing credentials:

```bash
rm -vf ${HOME}/.aws/credentials
```

Install jq. We will use this to help us process json.

```bash
sudo yum install -y jq
```

Upgrade AWS CLI:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Configure AWS CLI with the current region as default:

```bash
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```

Verify that AWS_REGION is set correctly:

```bash
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

Save the AWS_ACCOUNT_ID and AWS_REGION to the bash_profile:

```bash
echo "export AWS_ACCOUNT_ID=${AWS_ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

Verify the that the Cloud9 IDE is configured to use the correct IAM role:

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-role -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

If the IAM role is not valid, **DO NOT PROCEED**. Go back and confirm the steps on this page.

### Increase the disk size on the Cloud9 instance

Copy the script below and paste it into your Cloud9 terminal:

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

_Note_: The command above adds more disk space to the root volume of the EC2 instance that Cloud9 runs on. Once the command runs, the instance reboots which could take a minute or two to complete. When this completes you are ready to move on to the next step.
