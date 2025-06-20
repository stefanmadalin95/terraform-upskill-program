# 🧱 Exercise 2: Create a Reusable IAM Role Module

## Objective

Build a module to manage IAM roles.

---

## Steps

✅ Inside `modules/iam_role/`, define:

- `main.tf` – IAM role resource with `assume_role_policy`  
- `variables.tf` – accepts `role_name`  
- `outputs.tf` – returns role name and ARN

✅ Call it in root config like this:

```hcl
module "data_role" {
  source    = "./modules/iam_role"
  role_name = "data-ingestion-role"
}
```

✅ Apply and validate.

## Reflection
- How does this module help you enforce standards across teams?

---

➡️ **Next Exercise:** [🧪 Exercise 3: Compose Modules in a Root Project](./exercise-3.md)