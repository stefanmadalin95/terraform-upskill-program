# 📝 Exercise 3: Add Variables for Flexibility

## Objective

Use multiple variables to make your configuration even more reusable and dynamic.

---

## Steps

✅ Create a file `variables.tf` and add the following variables:

```hcl
variable "region" {
  description = "AWS region for deployment"
  default     = "eu-central-1"
}

variable "bucket_name" {
  description = "Name of the S3 bucket"
  default     = "my-first-data-lake-bucket"
}

variable "role_name" {
  description = "Name of the IAM role"
  default     = "data-processing-role"
}
```

✅ In `main.tf` and `provider.tf`, use the new variables:

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "data_bucket" {
  bucket = var.bucket_name
}

resource "aws_iam_role" "data_role" {
  name = var.role_name
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Action = "sts:AssumeRole",
      Effect = "Allow",
      Principal = {
        Service = "ec2.amazonaws.com"
      }
    }]
  })
}
```

✅ Re-run:

```bash
terraform plan
terraform apply
```

## Reflection
- How does using more variables make your code easier to reuse and share?
- What other variables might you want to add for future flexibility?

---

➡️ **Next Exercise:** [🧪 Exercise 4: Use Data Sources](./exercise-4.md)