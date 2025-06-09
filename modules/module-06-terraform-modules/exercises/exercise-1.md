# 📝 Exercise 1: Create a Local Module

## Objective

Practice creating a reusable local module.

---

## Steps

✅ Create a directory called `modules/my-s3-bucket/`.  
✅ Inside, create `main.tf` to define an S3 bucket resource.  
✅ Create `variables.tf` for `bucket_name`.  
✅ Create `outputs.tf` to output the bucket name.

✅ In your root module, reference this local module:

```hcl
module "my_s3" {
  source      = "./modules/my-s3-bucket"
  bucket_name = "my-reusable-bucket"
}
```

✅ Run:

```bash
terraform init
terraform plan
terraform apply
```

## Reflection
- How does this module structure make your code easier to manage?
- How would you document this module for your team?
- Write your answers here or discuss with your team!