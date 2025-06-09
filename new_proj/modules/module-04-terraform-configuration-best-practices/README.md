# 🏗️ Module 04: Terraform Configuration Best Practices

Welcome to **Module 04**! In this module, we’ll focus on writing **clean, maintainable, and scalable Terraform code**. By following best practices, you’ll ensure your infrastructure as code is robust and easier to manage.

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand recommended file structure and naming conventions  
✅ Learn the importance of formatting, comments, and documentation  
✅ Explore techniques for reusability and maintainability  
✅ Practice applying these best practices in small Terraform projects

---

## 🔧 Key Best Practices

### 1️⃣ File and Directory Structure

Organize your files for clarity and scalability:

main.tf
variables.tf
outputs.tf
terraform.tfvars

yaml
Copy
Edit

Use subfolders for modules or environments as your project grows.

---

### 2️⃣ Naming Conventions

✅ Use descriptive, consistent names for resources, variables, and outputs.  
✅ Avoid using generic names like `resource "aws_s3_bucket" "bucket1"`. Instead, use `resource "aws_s3_bucket" "logs_bucket"`.

---

### 3️⃣ Comments and Documentation

✅ Use comments to explain why something is done a certain way:

```hcl
# Create an S3 bucket for storing logs
resource "aws_s3_bucket" "logs_bucket" {
  bucket = "my-logs-bucket"
  acl    = "private"
}
✅ Keep README files updated for your modules!

4️⃣ Formatting and Linting
✅ Use terraform fmt to format your code consistently:

bash
Copy
Edit
terraform fmt
✅ Use linters like tflint for catching errors early.

5️⃣ Variable and Output Organization
✅ Keep variables in a separate variables.tf file.
✅ Group outputs in outputs.tf for easier discovery.

6️⃣ Keep Secrets Out of Code
✅ Use environment variables or secret managers (like AWS Secrets Manager).
✅ Avoid hardcoding sensitive data.

💡 Exercises
✅ Exercise 1: Organize Your Terraform Files
✅ Exercise 2: Clean Up and Format

🔗 References
Explore deeper best practices and examples in references.md.