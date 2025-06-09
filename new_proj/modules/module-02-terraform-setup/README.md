# ⚙️ Module 02: Terraform Setup

Welcome to **Module 02**! In this module, we’ll get your environment ready to start working with Terraform. Let’s roll up our sleeves and set up everything you need for smooth Terraform development!

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Install Terraform on your local machine  
✅ Configure AWS CLI and credentials  
✅ Verify your Terraform environment setup  
✅ Understand environment variables and basic configuration

---

## 🔧 Key Setup Steps

### 1️⃣ Install Terraform

Terraform is a single binary file that you can download from the [official website](https://developer.hashicorp.com/terraform/downloads).

#### Steps:
1. Download the binary for your operating system.  
2. Unzip it and place it in a directory on your `PATH`.  
3. Verify the installation:

```bash
terraform --version
```

### 2️⃣ Configure AWS CLI
Terraform interacts with AWS using the AWS CLI.
You’ll need the CLI installed and configured to let Terraform authenticate and manage your resources.

#### Steps:
Install the AWS CLI: Follow the installation guide for your OS.

#### Configure your AWS credentials:

```bash
aws configure
```

✅ Enter:
- AWS Access Key ID
- AWS Secret Access Key
- Default region name
- Output format (json, yaml, etc.)

Verify your credentials:

```bash
aws sts get-caller-identity
```
✅ If it shows your AWS account details, you’re all set!

### 3️⃣ Set Environment Variables (Optional but Recommended)
Terraform can also use environment variables to securely authenticate with AWS.

Example:
```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="eu-west-1"
```
✅ Use these for scripting or CI/CD setups.

### 4️⃣ Verify Everything
✅ Run:

```bash
terraform version
aws sts get-caller-identity
```
✅ If both commands work, your environment is ready for Terraform!