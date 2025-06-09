# 📝 Exercise 1: Create an S3 Bucket

## Objective

Deploy an S3 bucket for storing data lake files.

---

## Steps

✅ In your `main.tf`, define an S3 bucket resource with a unique name.  
✅ Add basic configurations like ACL and versioning.  
✅ Output the bucket name to verify deployment.

✅ Run:

```bash
terraform init
terraform apply
```

## Reflection
Why is S3 such a good fit for data lake storage?

How would you manage multiple buckets for different data layers (raw, processed, curated)?