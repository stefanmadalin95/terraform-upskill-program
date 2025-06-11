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

Providers are the **plugins** that Terraform uses to **communicate** with cloud platforms and APIs—like AWS, Azure, GCP, or even GitHub.

**Analogy:**  
Think of a **provider** as the **cloud “driver”** in your infrastructure “car”—without it, Terraform can’t reach the cloud.

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

Data sources in Terraform are **read-only lookups** to get information from your cloud environment or external services. They **don’t create resources**—they just **fetch existing data** for you to use.

**Analogy:**  
Think of data sources like **asking AWS for info** about something that’s already there—like the region name, an existing VPC, or your account ID.

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

## 🌟 Putting It All Together
Here’s how these pieces fit in a typical data engineering project:

1️⃣ Use the provider to connect to AWS
2️⃣ Create resources like S3 buckets
3️⃣ Use variables to make them flexible (like region or bucket name)
4️⃣ Use data sources to read existing data (like AWS account ID)
5️⃣ Show final outputs for your team to see
6️⃣ Terraform tracks everything in state file


## 💡 Exercises

Let’s put these concepts to practice:

✅ [Exercise 1: Configure the AWS Provider](exercises/exercise-1.md)  
✅ [Exercise 2: Create Multiple Resources](exercises/exercise-2.md)  
✅ [Exercise 3: Add Variables for Flexibility](exercises/exercise-3.md)  
✅ [Exercise 4: Use Data Sources](exercises/exercise-4.md)  
✅ [Exercise 5: Show Outputs](exercises/exercise-5.md)  
✅ [Exercise 6: Understand Terraform State](exercises/exercise-6.md)  

## 🔗 References
Check out additional resources for deeper understanding in [references.md](references.md).

## 🎉 Ready for the Next Step?
✅ Once you’re set up, proceed to [Module 04: Terraform Configuration & Best Practices](../module-04-terraform-configuration-best-practices/README.md).