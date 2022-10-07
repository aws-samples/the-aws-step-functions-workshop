---
title: 'AWS Cloud9 Workspace Setup'
weight: 133
---

:::alert{header="Important" type="warning"}
If you just completed the Cloud9 set up for Module 10 Deploy with AWS CDK, please navigate to the Cloud9 workspace management page and select **stepfunctionsworkshop-sam-role** from the **IAM Role** drop down, and select **Save**
If you did not just complete Module 10, please continue with the instructions below.
:::

- Log into the AWS Console
- Navigate to [AWS Cloud9](https://console.aws.amazon.com/cloud9/home) in the console. Make sure you are in the correct region.
- Select **StepFunctionsWorkshop** from the environment list and click **Open IDE** button. Maximize the terminal display by closing the **welcome tab** and the **lower work area**. Open a new **terminal** tab in the main work area:
  ![AWS Cloud9 Before](/static/img/setup/c9before.png)
- Your workspace should now look like this:
  ![AWS Cloud9 After](/static/img/setup/c9after.png)

### Attach a role to the AWS Cloud9 EC2 instance

- From your **AWS Cloud9** IDE, click on **Manage EC2 Instance** in the top right menu as shown in the diagram below.
  ![AWS Cloud9 manage](/static/img/setup/c9manageinstance.png)
- Select the AWS Cloud9 instance by checking the box next to it, then choose **Actions / Security / Modify IAM Role**
  ![AWS Cloud9 instance role](/static/img/setup/c9instancerole.png)
- Choose **stepfunctionsworkshop-sam-role** from the **IAM Role** drop down, and select **Save**
- Return to your workspace and click the sprocket, or launch a new tab to open the Preferences tab
- Select **AWS Settings** in the left navigation.
- Turn off **AWS managed temporary credentials**
- Close the Preferences tab
  ![AWS Cloud9 aws settings](/static/img/setup/c9disableiam.png)

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

Verify the that the AWS Cloud9 IDE is configured to use the correct IAM role:

```bash
aws sts get-caller-identity --query Arn | grep stepfunctionsworkshop-role -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

If the IAM role is not valid, **DO NOT PROCEED**. Go back and confirm the steps on this page. If the role is valid click **Next**.
