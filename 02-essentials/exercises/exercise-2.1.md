# 🧪 Exercise 2.1: Using Variables and Outputs with AWS S3 📦

## 🎯 Objective

Create an S3 bucket using variables and display its name and region as outputs.

## ✅ Tasks

1. Create a directory named `exercise-2.1`.
2. Inside that directory, create the following files:

### 📄 `variables.tf`

```hcl
variable "bucket_name" {
  description = "The name of the S3 bucket."
  default     = "my-simple-terraform-bucket"
}

variable "region" {
  description = "The AWS region to create the bucket in."
  default     = "us-east-1"
}
```

### 📄 `main.tf`

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name
  acl    = "private"
}
```

### 📄 `outputs.tf`

```hcl
output "bucket_name" {
  value = aws_s3_bucket.example.bucket
}

output "bucket_region" {
  value = var.region
}
```

## ▶️ Steps to Run

```bash
terraform init
terraform plan
terraform apply
```

🧼 When done, clean up with:

```bash
terraform destroy
```

---

✅ You just created your first AWS resource using variables and outputs!
