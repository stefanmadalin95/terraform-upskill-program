# 📝 Exercise 4: Apply and Inspect Your Infra

## Objective

Deploy your resources and see the final result.

---

## Steps

✅ Run:

```bash
terraform apply
```
✅ Confirm when prompted

✅ Add this to outputs.tf:

```hcl
output "bucket_name" {
  value = aws_s3_bucket.data_bucket.bucket
}
```

✅ Run:

```bash
terraform output
```

## Reflection
- How would this output help your teammates or downstream apps?