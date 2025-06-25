# 📝 Exercise 3: Add Variables and Locals for Flexibility

## Objective

Use multiple variables and locals to make your configuration more reusable, readable, and maintainable.


---

## Steps

✅ Create a file `variables.tf` and add the following variables:

```hcl
variable "region" {
  description = "AWS region for deployment"
  default     = "eu-west-1"
}

variable "bucket_prefix" {
  description = "Name of the S3 bucket"
  default     = "my-first"
}

variable "environment" {
  description = "Deployment environment (e.g. dev, staging, prod)"
  default     = "dev"
}

variable "role_name" {
  description = "Name of the IAM role"
  default     = "data-processing-role"
}
```

✅ Create a new file called locals.tf and define your locals:

```hcl
locals {
  bucket_name = "${var.bucket_prefix}-data-lake-${var.environment}"
}
```

✅ In `main.tf` and `provider.tf`, use the new variables:

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "data_bucket" {
  bucket = local.bucket_name
}

resource "aws_iam_role" "data_role" {
  name = var.role_name

  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Action = "sts:AssumeRole",
      Effect = "Allow",
      Principal = {
        Service = "glue.amazonaws.com"
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