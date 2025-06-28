# 🪣 Exercise 1: Provision Data Lake Buckets and Folders

## 🎯 Objective

Create an S3 bucket with folder-like prefixes for the **raw** and **processed** layers of the data lake. These will be the foundation of your architecture in the next module.

---

## 🧱 What You’ll Build

You’ll provision:

- One S3 bucket to represent the data lake
- Two directories (`raw/`, `processed/`)
- Versioning and server-side encryption
- Tagging for environment and ownership

---

## 🪜 Steps

### ✅ Step 1: Create a New Module (if needed)

Inside `modules/s3_data_lake_bucket/`:

#### `main.tf`

```hcl
resource "aws_s3_bucket" "data_lake" {
  bucket = var.bucket_name

  versioning {
    enabled = true
  }

  server_side_encryption_configuration {
    rule {
      apply_server_side_encryption_by_default {
        sse_algorithm = "AES256"
      }
    }
  }

  tags = var.tags
}
```

### ✅ Step 2: Add Folder Markers (objects with / suffix)

```hcl
resource "aws_s3_object" "raw_folder" {
  bucket = aws_s3_bucket.data_lake.id
  key    = "raw_data/"
}
```

### ✅ Step 3: Add Variables and Outputs

- variables.tf

```hcl
variable "bucket_name" {
  description = "Name of the data lake bucket"
  type        = string
}

variable "tags" {
  description = "Tags to apply to the bucket"
  type        = map(string)
}
```

- outputs.tf

```hcl
output "bucket_name" {
  value = aws_s3_bucket.data_lake.bucket
}
```

### ✅ Step 4: Call the Module
In your root configuration:


```hcl
module "data_lake_bucket" {
  source      = "./modules/s3_data_lake_bucket"
  bucket_name = "data-lake-upskill-${random_id.suffix.hex}"
  tags = {
    environment = "dev"
    owner       = "data-team"
    module      = "data-lake"
  }
}
```

###  🔁 Run the Workflow

```bash
terraform init
terraform plan
terraform apply
```

## 🧠 Reflection
- Why are we using prefixes like raw/ and /processed instead of separate buckets?
- How does Terraform help ensure that these conventions stay consistent across environments?
- What other lifecycle policies or configurations might you want to apply to these buckets in a real data lake?

---

➡️ **Next Exercise:** [🧪 Exercise 2: Create Glue Catalog Database and Table](./exercise-2.md)