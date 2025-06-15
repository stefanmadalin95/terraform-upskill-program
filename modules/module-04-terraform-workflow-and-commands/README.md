# 🚀 Module 04: Terraform Commands – From Zero to Hero

Now that you've built some Terraform code, it's time to take control with the **commands** that bring everything to life. In this module, you'll learn how to run, validate, and destroy infrastructure—**safely and confidently.**

---

## 📖 Learning Objectives

By the end of this module, you’ll:

✅ Understand the **purpose** of each core Terraform CLI command  
✅ Know **when** to use which command and **why**  
✅ Practice these commands using real examples from previous modules  
✅ Build good habits that prepare you for collaborative infrastructure work

---

## 🛠️ Commands You’ll Master

Here’s what we’ll cover:

| Command         | What It Does                                           | When to Use                         |
|----------------|--------------------------------------------------------|-------------------------------------|
| `terraform init` | Initializes project, downloads providers               | When starting a new config or after backend changes |
| `terraform validate` | Checks for syntax errors and configuration issues   | Before running plan/apply           |
| `terraform fmt`     | Formats Terraform code to the standard style        | After writing/editing code          |
| `terraform plan`    | Shows what Terraform will do before applying        | Before any apply                    |
| `terraform apply`   | Applies the planned changes to your infrastructure  | When you're ready to deploy         |
| `terraform destroy` | Destroys everything Terraform created               | For cleanup or tearing down envs    |
| `terraform output`  | Shows values from your output blocks                | To retrieve deployed resource info  |
| `terraform show`    | Displays what's inside the state file               | For debugging and understanding     |

---

## 🔁 Lifecycle of Terraform in Action

1️⃣ Write your code (`.tf` files)  
2️⃣ Run `terraform init` once  
3️⃣ Format and validate: `terraform fmt`, `terraform validate`  
4️⃣ Preview with `terraform plan`  
5️⃣ Deploy with `terraform apply`  
6️⃣ Retrieve key info with `terraform output`  
7️⃣ Destroy with `terraform destroy` if needed

Think of it as your **developer loop** when managing infrastructure.

---

## 📁 Exercises

👉 Head over to the [exercises folder](./exercises) to try each command in action.

✅ [Exercise 1: Initialize Your Project (`terraform init`)](exercises/exercise-1.md)  
✅ [Exercise 2: Validate and Format Code](exercises/exercise-2.md)  
✅ [Exercise 3: Plan Infrastructure Changes](exercises/exercise-3.md)  
✅ [Exercise 4: Apply and Output](exercises/exercise-4.md)  
✅ [Exercise 5: Tear Down With Destroy](exercises/exercise-5.md)

---

## 🧠 Best Practices

✅ Always run `terraform validate` before applying  
✅ Use `terraform plan` to preview changes and avoid surprises  
✅ Use `terraform output` to extract important info for CI/CD pipelines or documentation  
✅ Don’t forget `terraform destroy` for cleaning up learning environments

## 🔗 References
Explore deeper best practices and examples in [references](references.md).

---

## 🧭 Ready to Learn State?

Once you're comfortable with the command line flow, continue to [Module 05: Terraform State Management](../module-05-terraform-state-management/README.md) to understand how Terraform tracks everything you've built.

Let’s keep building momentum! 💥