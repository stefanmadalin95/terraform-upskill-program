# 📦 Module 06: Terraform Modules

Welcome to **Module 06**! In this module, we’ll explore how to create and use **Terraform modules** to make your configurations more **reusable, organized, and collaborative**.

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand what **Terraform modules** are and why they matter  
✅ Learn how to create a **local module**  
✅ Explore how to use **public modules** from the Terraform Registry  
✅ Practice building and using modules for real-world infrastructure

---

## 🧩 Key Concepts

### 1️⃣ What are Modules?

Modules are containers for multiple Terraform resources that work together.  
✅ They help you **organize** and **reuse** your code.

---

### 2️⃣ Why Use Modules?

✅ DRY (Don’t Repeat Yourself): Reuse the same configurations.  
✅ Scalability: Easily scale your infrastructure by reusing modules.  
✅ Collaboration: Modules are easier to share and maintain.

---

### 3️⃣ Creating a Local Module

A simple **module structure**:

- modules/
- my-s3-bucket/
- main.tf
- variables.tf
- outputs.tf

In your **root configuration**:

```hcl
module "s3_bucket" {
  source = "./modules/my-s3-bucket"
  bucket_name = "my-team-logs"
}
```

### 4️⃣ Using Modules from the Terraform Registry
You can also use pre-built modules:

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.0.0"
  name    = "my-vpc"
  cidr    = "10.0.0.0/16"
}
```

### 5️⃣ Best Practices

✅ Keep your modules small and focused.
✅ Use input variables to make them flexible.
✅ Document how to use them in a README.md file.
✅ Use version pinning when using modules from the Registry.

## 💡 Exercises
✅ [Exercise 1: Create a Local Module](exercises/exercise-1.md)
✅ [Exercise 2: Use a Public Module](exercises/exercise-2.md)

## 🔗 References
Check out additional resources and examples in [references.md](references.md).

## 🎉 Ready for the Next Step?
✅ Once you’re comfortable with modules, proceed to [Module 07: AWS Data Lake Architecture and Components](../module-07-aws-data-lake-architecture-and-components/README.md).

Keep your modules clean and your infrastructure consistent! 🚀✨