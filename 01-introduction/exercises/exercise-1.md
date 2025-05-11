# Exercise 1: Getting Started with Terraform

## Objectives

- Install Terraform on your local machine
- Verify the installation
- Explore basic Terraform commands
- Create your first configuration file

## Tasks

### 1. Install Terraform

Follow the official installation guide based on your operating system:
- [Terraform Installation Guide](https://learn.hashicorp.com/tutorials/terraform/install-cli)

### 2. Verify Installation

Run the following command to verify Terraform is installed correctly:
```bash
terraform version
```

### 3. Explore Basic Commands

Run the following commands and observe the output:
```bash
terraform -help
terraform -help plan
terraform -help apply
```

### 4. Create Your First Configuration

1. Create a new directory for your first Terraform project
2. Create a file named `main.tf` with the following content:

```hcl
terraform {
  required_providers {
    local = {
      source = "hashicorp/local"
      version = "~> 2.0"
    }
  }
}

resource "local_file" "hello" {
  content  = "Hello, Terraform!"
  filename = "${path.module}/hello.txt"
}
```

3. Run the following commands:

```bash
terraform init
terraform plan
terraform apply
```

4. Verify that a file named `hello.txt` has been created with the content "Hello, Terraform!"

## Submission

Document your process and any observations or challenges you encountered.
