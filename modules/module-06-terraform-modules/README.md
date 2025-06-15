# 🧱 Module 06: Working with Terraform Modules

Welcome to Module 06! Terraform modules are one of the most powerful features for writing **clean**, **reusable**, and **scalable** infrastructure code.

You’ve already seen Terraform in action using `.tf` files. Now, it’s time to learn how to **package** that knowledge into modules—just like you write functions in code to avoid duplication.

---

## 📖 Learning Objectives

✅ Understand the purpose of modules in Terraform  
✅ Learn how to structure and call both **local** and **remote** modules  
✅ Build your own module to manage S3 buckets and IAM roles  
✅ Practice splitting reusable logic into self-contained building blocks  
✅ Prepare for organizing infrastructure in your **data lake project**

---

## 🔍 What Is a Module?

A **module** is simply a collection of `.tf` files in a folder. You can think of it as:

📦 **A reusable Terraform package**

✅ Modules allow you to:
- Group related resources (e.g., all resources for a data ingestion job)
- Pass in variables to customize behavior
- Reduce duplication across environments (dev, test, prod)

---

### 🧠 Analogy

Think of a module like a **reusable Lego block**:  
You design it once, and then use it over and over again in different builds.

---

## 🧩 Module Structure

Every module can contain:
📁 /my-module/  
├── main.tf # resource definitions  
├── variables.tf # input parameters  
├── outputs.tf # what the module returns  


And you call it like this:

```hcl
module "my_bucket" {
  source = "./modules/s3_bucket"

  bucket_name = "modular-bucket-001"
  region      = "eu-central-1"
}
```

## 🧠 Best Practices  
✅ Keep modules focused – do one thing well (e.g., an S3 bucket, an IAM role)  
✅ Use meaningful variable names and clear outputs  
✅ Store reusable modules in a central modules/ folder  
✅ Avoid tight coupling between unrelated modules  

## 🛠️ What You'll Build

In this module, you'll:

- Create a module for S3 bucket provisioning
- Create a module for IAM role definition
- Use a root configuration to call both modules
- Pass in variables and access outputs
- Reflect on how this structure helps scale your infrastructure

## 💡 Exercises

👉 Go to the exercises folder to start building:

✅ [Exercise 1: Create a Reusable S3 Bucket Module](exercises/exercise-1.md)  
✅ [Exercise 2: Create a Reusable IAM Role Module](exercises/exercise-2.md)  
✅ [Exercise 3: Compose Modules in a Root Project](exercises/exercise-3.md)  
✅ [Exercise 4: Use Module Outputs](exercises/exercise-4.md)  
✅ [Exercise 5: Reflect on Modular Infrastructure](exercises/exercise-5.md)    

## 🔗 References
Explore deeper best practices and examples in [references](references.md).

## 🎉 Ready for the Next Step?
✅ Once you’re set up, proceed to [Module 07: Intro to Data Lake Components](../module-07-data-lake-components/README.md).