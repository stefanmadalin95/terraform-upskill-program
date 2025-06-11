# 📝 Exercise 3: Configure AWS CLI and Credentials

## Objective

Terraform interacts with AWS using the AWS CLI.
You’ll need the CLI installed and configured to let Terraform authenticate and manage your resources.

---

## Steps
Install the AWS CLI: Follow the installation guide for your OS.

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