# 💾 Module 05: Terraform State Management

Welcome to **Module 05**! In this module, you’ll dive into how Terraform tracks the infrastructure it manages—and how to **secure and share** that information for team-based development.

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand what the **Terraform state file** is and why it’s critical  
✅ Learn the risks of local state in team environments  
✅ Configure **remote state storage in S3**  
✅ Set up **state locking with DynamoDB** (optional but recommended)  
✅ Practice using a **project-like structure** with multiple `.tf` files and modules

---

## 🧠 What Is Terraform State?

When you deploy infrastructure with Terraform, it keeps a **record of what it deployed** in a file called `terraform.tfstate`.

✅ This file tracks:
- Resource names and IDs
- Dependencies
- Metadata

✅ Without the state, Terraform wouldn't know what already exists.

---

## 🚨 Why Managing State Matters

🟡 In solo projects, a local `terraform.tfstate` file is fine.  
🔴 In **team settings**, storing state locally is dangerous:
- It can get **out of sync**
- It can be **accidentally overwritten**
- It doesn't support collaboration

✅ The solution: store state **remotely in S3** with **locking via DynamoDB**

---

## ☁️ Remote State in S3

### 1️⃣ Set up an S3 bucket to hold your state

```hcl
resource "aws_s3_bucket" "tf_state" {
  bucket = "terraform-state-yourname"
  acl    = "private"
}
```

### 2️⃣ Optional: Create a DynamoDB table for locking

```hcl
resource "aws_dynamodb_table" "tf_locks" {
  name           = "terraform-state-locks"
  billing_mode   = "PAY_PER_REQUEST"
  hash_key       = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

### 3️⃣ Configure your backend in a new backend.tf

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-state-yourname"
    key            = "dev/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-state-locks"
    encrypt        = true
  }
}
```

🔄 Putting It All Together
Let’s structure this like a real project:

📁 /project-root  
├── main.tf – resources  
├── variables.tf – configuration  
├── outputs.tf – final values  
├── backend.tf – state config  
└── provider.tf – AWS provider  

## 💡 Exercises

✅[Exercise 1: Explore Local Terraform State](exercises/exercise-1.md)  
✅[Exercise 2: Set Up Remote Backend in S3](exercises/exercise-2.md)  
✅[Exercise 3: Add DynamoDB Locking (Optional)](exercises/exercise-3.md)  
✅[Exercise 4: Simulate a Mini Project Setup](exercises/exercise-4.md)  

## 🔗 References
Explore deeper best practices and examples in [references](references.md).

## 🎉 Ready for the Next Step?
✅ Once you’re set up, proceed to [Module 06: Terraform Workflow and Commands](../module-06-terraform-modules/README.md).