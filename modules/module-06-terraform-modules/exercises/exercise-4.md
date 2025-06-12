# 🧱 Exercise 4: Use Module Outputs

## Objective

Capture outputs from modules and use them in other modules or pipelines.

---

## Steps

✅ Use `output.tf` in the root to export module outputs:

```hcl
output "bucket_name" {
  value = module.my_bucket.bucket_name
}
```

✅ Run:

```bash
terraform output
```

✅ View and verify output values

## Reflection
- How could this help you pass info between modules or external systems?