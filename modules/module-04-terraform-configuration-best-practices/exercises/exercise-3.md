# 📝 Exercise 3: Add DynamoDB Locking (Optional)

## Objective

Prevent team members from accidentally applying at the same time.

---

## Steps

✅ Create the DynamoDB table manually or via Terraform

✅ Add this to `backend.tf`:

```hcl
dynamodb_table = "terraform-state-locks"
```

✅ Re-run:

```bash
terraform init
```

✅ Test locking: Run terraform apply in two terminals.

## Reflection
- Why is locking important in a CI/CD pipeline?
- Have you ever seen inconsistent environments due to parallel changes?