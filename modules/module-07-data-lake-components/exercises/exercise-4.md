# 🔐 Exercise 4: Create IAM Role for Catalog Access

## 🎯 Objective

Create an IAM role that AWS Glue and Athena can assume to access your data lake stored in S3. This role will include a trust policy and a permissions policy tailored for this use case.

---

## 🧱 What You’ll Build

- An **IAM Role** trusted by Glue or Athena
- An **inline policy** allowing read/write access to the data lake S3 bucket
- Outputs to expose the role name and ARN

---

## 🪜 Steps

### ✅ Step 1: Create a New Module

Create a module called `iam_glue_data_access/`.

#### `main.tf`

```hcl
resource "aws_iam_role" "glue_access" {
  name = var.role_name

  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Effect = "Allow",
      Principal = {
        Service = var.service_principal
      },
      Action = "sts:AssumeRole"
    }]
  })

  tags = var.tags
}

resource "aws_iam_role_policy" "s3_access" {
  name = "glue-s3-access"
  role = aws_iam_role.glue_access.id

  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect = "Allow",
        Action = [
          "s3:GetObject",
          "s3:ListBucket"
        ],
        Resource = [
          "arn:aws:s3:::${var.bucket_name}",
          "arn:aws:s3:::${var.bucket_name}/*"
        ]
      }
    ]
  })
}
```

### ✅ Step 2: Define Variables and Outputs

#### `variables.tf`

```hcl
variable "role_name" {
  description = "IAM role name"
  type        = string
}

variable "service_principal" {
  description = "Service principal to allow (e.g., glue.amazonaws.com)"
  type        = string
}

variable "bucket_name" {
  description = "Name of the S3 bucket the role can access"
  type        = string
}

variable "tags" {
  description = "Standard tags"
  type        = map(string)
}
```

#### `outputs.tf`

```hcl
output "iam_role_name" {
  value = aws_iam_role.glue_access.name
}

output "iam_role_arn" {
  value = aws_iam_role.glue_access.arn
}
```

### ✅ Step 3: Call the Module

In your root configuration:

```hcl
module "glue_iam_role" {
  source            = "./modules/iam_glue_data_access"
  role_name         = "glue-data-access-role"
  service_principal = "glue.amazonaws.com"
  bucket_name       = module.unique_bucket.bucket_name
  tags = {
    environment = "dev"
    owner       = "data-team"
    module      = "iam"
  }
}
```

#### 🔁 Run the Workflow

```bash
terraform init
terraform plan
terraform apply
```

## 🧠 Reflection
- Why is it important to scope S3 permissions tightly in IAM policies?
- What could go wrong if this role were assumed by other AWS services?
- How would you update this policy to include other buckets or actions?