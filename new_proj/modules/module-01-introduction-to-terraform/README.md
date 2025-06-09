# 🌱 Module 01: Introduction to Terraform

Welcome to your first step in the **Terraform Upskill Program**! 🎉  
In this module, we’ll explore what Terraform is, why it matters, and how it fits into the world of Infrastructure as Code (IaC).

---

## 📖 Learning Objectives

By the end of this module, you will:

✅ Understand what Infrastructure as Code (IaC) is  
✅ Learn what Terraform is and its key benefits  
✅ Identify core components of Terraform  
✅ Recognize how Terraform integrates with AWS and Data Engineering projects  

---

## 🧩 Key Concepts

### 1️⃣ What is Infrastructure as Code (IaC)?

**IaC** is the practice of managing infrastructure (like networks, virtual machines, and data storage) using machine-readable configuration files instead of manual processes.

**Benefits:**
- Automation of deployments
- Consistency and reproducibility
- Easy to track and version in Git

👉 **Deep Dive:** [What is Infrastructure as Code (IaC)?](iac-overview.md)

---

### 2️⃣ What is Terraform?

**Terraform** is an open-source tool by HashiCorp that enables you to **provision and manage infrastructure** using a declarative language called **HCL** (HashiCorp Configuration Language).

**Why we love Terraform:**
✅ Works across different clouds (AWS, Azure, GCP, etc.)  
✅ Easy to learn and write  
✅ Promotes collaboration and best practices  

---

### 3️⃣ Terraform Core Components

| Component | Description |
|-----------|-------------|
| **Providers** | Interface to cloud platforms and services (e.g., AWS, Azure, GCP) |
| **Resources** | Actual infrastructure objects (e.g., EC2 instances, S3 buckets) |
| **Data Sources** | Read data from other systems for use in your config |
| **Variables** | Inputs to make your code reusable and flexible |
| **Outputs** | Display useful information after deployment |
| **State** | Keeps track of deployed resources and their status |

---

### 4️⃣ Why Should Data Engineers Care?

Data engineering workflows rely heavily on cloud infrastructure:

✅ Data lakes in S3  
✅ ETL jobs in Glue  
✅ Networking via VPC and IAM  

Terraform **automates and secures** the deployment of these resources, letting you focus on **data pipelines and analytics**!

---

## 🚀 Practical Example

Here’s a sneak peek at a **simple Terraform configuration** to create an S3 bucket:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example_bucket" {
  bucket = "terraform-upskill-example"
  acl    = "private"
}
```

## 💡 Exercises

Ready to roll up your sleeves?  
Complete these exercises to reinforce your learning:

✅ [Exercise 1: Understand IaC and Terraform](exercises/exercise-1.md)  
✅ [Exercise 2: Explore the core components of Terraform](exercises/exercise-2.md)

Each exercise includes a short challenge and reflection questions—**discuss with a colleague to maximize learning!**