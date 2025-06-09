# 📝 Exercise 2: Use a Public Module

## Objective

Learn to use a module from the Terraform Registry.

---

## Steps

✅ Visit the [Terraform Registry](https://registry.terraform.io/).  
✅ Choose a module (like the `terraform-aws-modules/vpc/aws`).  
✅ In your `main.tf`, add:

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.0.0"
  name    = "my-team-vpc"
  cidr    = "10.0.0.0/16"
}
```

✅ Initialize and apply:

```bash
terraform init
terraform plan
terraform apply
```

## Reflection
- What’s the advantage of using a pre-built module from the Registry?
- How would you decide between using a public module or writing your own?
- Capture your thoughts here or share with the team!