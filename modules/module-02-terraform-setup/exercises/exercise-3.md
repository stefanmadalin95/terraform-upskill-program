# 📝 Exercise 3: Configure AWS CLI and Credentials

## Objective

Terraform interacts with AWS using the AWS CLI.
You’ll need the CLI installed and configured to let Terraform authenticate and manage your resources.

---

## Steps

### 🔐 Generate Access Keys in AWS Console

If you're using an IAM user to authenticate locally, you must generate access keys from the AWS Console. These keys allow Terraform and the AWS CLI to authenticate requests.

#### ✅ Step-by-Step Instructions:

- Log in to the AWS Management Console using your IAM user account.
- Navigate to Services → IAM (Identity and Access Management).
- In the left panel, click on Users.
- Click on your IAM username.
- Go to the Security credentials tab.
- Scroll down to the Access keys section.
- Click Create access key.
- When prompted, choose the use case:
- Select "Command Line Interface (CLI)"
- Click Next
- You’ll see the Access key ID and Secret access key.

⚠️ Make sure to copy the secret access key right away. You won’t be able to retrieve it again later.

Save them securely in a password manager or credentials file.

### Configure your AWS credentials:

```bash
aws configure
```

✅ Enter:
- AWS Access Key ID - **Retrieved from AWS**
- AWS Secret Access Key - **Retrieved from AWS**
- Default region name - **eu-west-1**
- Output format (json, yaml, etc.) - **Optional**

### Verify your credentials:

```bash
aws sts get-caller-identity
```

✅ If it shows your AWS account details, you’re all set!

---

➡️ **Next Exercise:** [🧪 Exercise 4: Install and Use Git](./exercise-4.md)