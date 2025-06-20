# 📝 Exercise 5: Show Outputs

## Objective

Display important info for your team.

---

## Steps

✅ Add an output for the bucket name:

```hcl
output "bucket_name" {
  value = aws_s3_bucket.data_bucket.id
}
```

✅ Apply:

```bash
terraform apply
```

✅ See the output in your terminal.

## Reflection
- Why is it useful to have outputs after deployment?

---

➡️ **Next Exercise:** [🧪 Exercise 6: Understand Terraform State](./exercise-6.md)