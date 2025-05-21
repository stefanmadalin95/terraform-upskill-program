# 🧪 Exercise 1: Getting Started with Terraform on AWS ☁️

## 🎯 Objectives

* 🛠️ Install Terraform on your local machine
* ✅ Verify the installation
* 🧪 Explore basic Terraform commands
* 🧰 Create your first AWS-based configuration file

---

## ✅ Tasks

### 🔹 1. Install Terraform

Follow the official guide to install Terraform based on your OS:
👉 [Terraform Installation Guide](https://learn.hashicorp.com/tutorials/terraform/install-cli)

---

### 🔹 2. Verify Installation

Run the following command to check the installation:

```bash
terraform version
```

✅ You should see the installed version displayed.

---

### 🔹 3. Explore Basic Terraform Commands

Run the following to understand what each command does:

```bash
terraform -help
terraform -help plan
terraform -help apply
```

📘 Take note of what each command is used for.

---

### 🔹 4. Create Your First AWS Configuration 🚀

1. Create a new folder for your Terraform project:

```bash
mkdir terraform-aws-intro && cd terraform-aws-intro
```

2. Create a file named `main.tf` with the following content:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-terraform-intro-bucket-${random_id.bucket_id.hex}"
  acl    = "private"
}

resource "random_id" "bucket_id" {
  byte_length = 4
}
```

3. Initialize and apply the configuration:

```bash
terraform init
terraform plan
terraform apply
```

🔐 Make sure your AWS credentials are configured. [How to Retrieve AWS Keys](../aws-access-keys.md)

4. Go to your AWS Console and verify that the S3 bucket has been created!

---

## 📄 Submission

✍️ Document:

* What steps you took
* What worked/didn’t work
* Screenshots or logs if possible

✅ Optional: Try deleting the bucket using:

```bash
terraform destroy
```

---

Great job! You’ve taken your first step into real AWS infrastructure using Terraform! 🎉
