# 🧱 Exercise 1: Create a Reusable S3 Bucket Module

## Objective

Build a module to create S3 buckets dynamically.

---

## Steps

✅ Inside `modules/s3_bucket/`, create:

- `main.tf` – contains the `aws_s3_bucket` resource  
- `variables.tf` – defines `bucket_name`
- `outputs.tf` – returns the bucket name

✅ In your root `main.tf`, call the module:

```hcl
module "my_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "upskill-s3-module-demo"
}
```
✅ Run:

```bash
terraform init
terraform apply
```

## Reflection
- How does using this module simplify reuse across environments?