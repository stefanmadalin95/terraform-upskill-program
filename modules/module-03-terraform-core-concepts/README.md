# 📦 Module 03: Terraform Core Concepts

Welcome to **Module 03**! In this module, we’ll explore the **fundamental building blocks of Terraform**. These concepts are essential to understanding how Terraform automates infrastructure and how you’ll use it in your data engineering work.

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand the purpose of **providers**, **resources**, and **data sources**  
✅ Work with **variables** and **outputs** to create dynamic configurations  
✅ Learn how **Terraform state** tracks your infrastructure  
✅ See real-world examples of these concepts in action

---

## 🧩 Key Concepts

### 1️⃣ Providers

Providers are plugins that let Terraform interact with cloud platforms and other services (like AWS, Azure, GCP).

**Example:**

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

### 2️⃣ Resources

Resources are the actual infrastructure components you create (like S3 buckets, IAM roles, or EC2 instances).

**Example:**

```hcl
resource "aws_s3_bucket" "example_bucket" {
  bucket = "my-terraform-bucket"
  acl    = "private"
}
```

### 3️⃣ Data Sources

Data sources let you fetch information from other resources or services to use in your Terraform configuration.

**Example:**

```hcl
data "aws_caller_identity" "current" {}
```

### 4️⃣ Variables

Variables make your configurations flexible and reusable.

**Example:**

```hcl
variable "region" {
  description = "AWS region to deploy resources"
  default     = "eu-west-1"
}
```

Use it in a configuration:

```hcl
provider "aws" {
  region = var.region
}
```

### 5️⃣ Outputs

Outputs display important information after your deployment—like bucket names, IDs, or URLs.

**Example:**

```hcl
output "bucket_name" {
  value = aws_s3_bucket.example_bucket.bucket
}
```

### 6️⃣ State

Terraform keeps track of everything it creates in a state file (```terraform.tfstate```).

This ensures Terraform knows the current status of your infrastructure.


## 🚀 Real-World Example

Here’s a basic example combining these concepts:

```hcl
provider "aws" {
  region = var.region
}

variable "region" {
  default = "eu-west-1"
}

resource "aws_s3_bucket" "data_bucket" {
  bucket = "my-data-lake-bucket"
  acl    = "private"
}

output "bucket_name" {
  value = aws_s3_bucket.data_bucket.id
}
```

## 💡 Exercises

Let’s put these concepts to practice:

✅ [Exercise 1: Define Your First Resource](exercises/exercise-1.md)
✅ [Exercise 2: Use a Data Source](exercises/exercise-2.md)

## 🔗 References
Check out additional resources for deeper understanding in [references.md](references.md).

## 🎉 Ready for the Next Step?
✅ Once you’re set up, proceed to [Module 03: Terraform Configuration & Best Practices](../module-04-terraform-configuration-best-practices/README.md).