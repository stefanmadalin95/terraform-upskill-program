# 📝 Exercise 1: Configure the AWS Provider

## Objective

Set up the **AWS provider** to connect Terraform to your AWS account.

---

## Steps

✅ Create a file called `provider.tf`.  
✅ Add the **provider block**:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "eu-west-1"
}
```

✅ Initialize Terraform:

```bash
terraform init
```

✅ Verify no errors.

## Reflection
- Why does Terraform need a provider block?
- How would you change this for another cloud (like Azure)?

---

➡️ **Next Exercise:** [🧪 Exercise 2: Create Multiple Resources](./exercise-2.md)
