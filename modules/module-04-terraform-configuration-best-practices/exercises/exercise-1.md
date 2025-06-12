# 📝 Exercise 1: Explore Local Terraform State

## Objective

Understand how Terraform tracks resources locally.

---

## Steps

✅ Apply a basic config from previous modules  
✅ Open `terraform.tfstate` (read-only!)  
✅ Run:

```bash
terraform state list
terraform state show aws_s3_bucket.data_bucket
```

✅ Observe the structure and data in the state

## Reflection
- What surprised you about what Terraform stores in the state?
- Why should this file be treated like sensitive configuration?