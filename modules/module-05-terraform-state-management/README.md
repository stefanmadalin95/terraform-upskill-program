# 💾 Module 05: Terraform State Management

Welcome to **Module 05**! In this module, you’ll dive into how Terraform tracks the infrastructure it manages—and how to **secure and share** that information for team-based development.

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand what the **Terraform state file** is and why it matters  
✅ Recognize the dangers of using local state in team environments  
✅ Learn how **remote state in S3** enables collaboration and reliability  
✅ See how **DynamoDB locking** prevents dangerous parallel actions  
✅ Practice applying these ideas in structured, modular projects  

---

## 🧠 What Is Terraform State?

Terraform's **state file** (`terraform.tfstate`) is a snapshot of your infrastructure. It’s how Terraform remembers what exists—so it can compare your `.tf` code to the real world.

✅ The state contains:  
- Resource IDs and metadata  
- Relationships between resources  
- Outputs and dependencies  

✅ Without it, Terraform would re-create or destroy resources unpredictably. It’s not just a file—it’s your single source of truth.

---

## 🚨 Why Managing State Matters

✅ Fine for solo projects  
If you’re building alone on your laptop, storing `terraform.tfstate` locally might seem good enough.

🔥 Problematic for teams

In team settings, local state quickly becomes a liability:
- Team members might overwrite each other’s state files
- CI/CD systems could break infrastructure if state is missing or outdated
- Debugging becomes a nightmare when state is inconsistent


## ☁️ Remote State: A Better Way to Collaborate

The solution is to store the state file **remotely**, in a shared, versioned location.
Terraform supports remote state backends like:

- **S3 (Amazon Simple Storage Service)** for durability and centralization
- **DynamoDB for locking**, preventing two people from applying at the same time

This setup allows teams to:
- Safely collaborate on infrastructure  
- Prevent race conditions  
- Enable automated pipelines  
- Maintain a clear audit trail  

## 🧪 What You’ll Practice in This Module
Instead of throwing more code at you here, we’ll explore remote state in action through guided exercises:

1️⃣ **Explore the local** `terraform.tfstate` file to understand what’s stored  
2️⃣ **Use a shared S3 bucket** (created by the course owner) to store state remotely  
3️⃣ **Enable state locking with DynamoDB** to simulate multi-user collaboration  
4️⃣ **Set up a real project structure** with best practices and per-user folders  

Each exercise builds your confidence with real-world tools—so when you’re in a team setting, you’ll already know how to set things up right.

## 💡 Exercises

✅[Exercise 1: Explore Local Terraform State](exercises/exercise-1.md)  
✅[Exercise 2: Set Up Remote Backend in S3](exercises/exercise-2.md)  
✅[Exercise 3: Add DynamoDB Locking (Optional)](exercises/exercise-3.md)  
✅[Exercise 4: Simulate a Mini Project Setup](exercises/exercise-4.md)  

## 🔗 References
Explore deeper best practices and examples in [references](references.md).

## 🎉 Ready for the Next Step?
✅ Once you’re set up, proceed to [Module 06: Terraform Workflow and Commands](../module-06-terraform-modules/README.md).