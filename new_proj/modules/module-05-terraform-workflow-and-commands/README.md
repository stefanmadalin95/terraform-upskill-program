# ⚙️ Module 05: Terraform Workflow and Commands

Welcome to **Module 05**! In this module, you’ll learn about the essential Terraform workflow and commands that let you deploy and manage infrastructure effectively.

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand the **standard Terraform workflow** (init, plan, apply, destroy)  
✅ Learn about additional commands for managing infrastructure  
✅ Practice using these commands in a real Terraform configuration  
✅ Build confidence in deploying and tearing down resources safely

---

## 🚀 Terraform Workflow

Here’s the typical Terraform lifecycle:

1️⃣ **Initialize**:  
```bash
terraform init
Downloads providers and sets up the project.

2️⃣ Plan:

bash
Copy
Edit
terraform plan
Previews the changes that Terraform will apply.

3️⃣ Apply:

bash
Copy
Edit
terraform apply
Applies the configuration and creates the resources.

4️⃣ Destroy:

bash
Copy
Edit
terraform destroy
Removes all resources managed by Terraform.

🔧 Additional Commands
✅ Show current state:

bash
Copy
Edit
terraform show
✅ Validate configuration:

bash
Copy
Edit
terraform validate
✅ Format code:

bash
Copy
Edit
terraform fmt
✅ List resources:

bash
Copy
Edit
terraform state list
💡 Best Practices
✅ Always run terraform plan before terraform apply.
✅ Use version control (like Git) to track changes.
✅ Document your workflows and share them with the team.
✅ Clean up resources you no longer need with terraform destroy.

💡 Exercises
✅ Exercise 1: Practice the Terraform Workflow
✅ Exercise 2: Troubleshoot and Destroy

🔗 References
Explore deeper explanations and command usage in references.md.