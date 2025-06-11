# 📝 Exercise 4: Use Data Sources

## Objective

Learn how to **query different data** from AWS with data sources.

---

## Steps

✅ In `main.tf`, add:

```hcl
data "aws_caller_identity" "current" {}
```

✅ Let’s add another data source: getting information about the AWS region.
```hcl
data "aws_region" "current" {}
```

✅ Add an output to display it:

```hcl
output "account_id" {
  value = data.aws_caller_identity.current.account_id
}

output "current_region" {
  value = data.aws_region.current.name
}
```

✅ Apply:

```bash
terraform apply
```

✅ See both outputs in the terminal!

## Reflection
- How do you think these data sources could help in your real-world data engineering projects?
- Can you think of other AWS data you’d want to query with Terraform?