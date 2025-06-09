# 🧪 Exercise 2.2: Creating Multiple IAM Users with `for_each` 👥

## 🎯 Objective

Use the `for_each` meta-argument to create multiple IAM users in a single configuration.

## ✅ Tasks

1. Create a directory named `exercise-2.2`.
2. Inside that directory, create the following files:

### 📄 `variables.tf`

```hcl
variable "user_names" {
  description = "List of IAM user names to create."
  type        = list(string)
  default     = ["alice", "bob", "charlie"]
}
```

### 📄 `main.tf`

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_iam_user" "users" {
  for_each = toset(var.user_names)

  name = each.value
  tags = {
    CreatedBy = "Terraform"
  }
}
```

### 📄 `outputs.tf`

```hcl
output "created_users" {
  value = [for user in aws_iam_user.users : user.name]
}
```

## ▶️ Steps to Run

```bash
terraform init
terraform plan
terraform apply
```

🧼 When done, clean up with:

```bash
terraform destroy
```

---

🙌 You now know how to dynamically create multiple IAM users with `for_each`!
