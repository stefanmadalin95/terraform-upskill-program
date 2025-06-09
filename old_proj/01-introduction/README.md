# Module 01: Introduction to Terraform 🌱

## 📖 Learning Objectives:

* Understand what Infrastructure as Code (IaC) is.
* Familiarize with the core concepts of Terraform.
* Understand when and why Terraform is used.

## 📚 Key Concepts:

1. What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is a practice where infrastructure (servers, networks, storage, etc.) is provisioned and managed using code and automation instead of manual processes.

📘 **Learn More:** [What is Infrastructure as Code (IaC)?](iac-overview.md)

### 2. What is Terraform?

Terraform is an open-source tool created by HashiCorp for defining and provisioning infrastructure resources using declarative code.

### 3. Terraform Core Components:

* **Providers:** Allow Terraform to manage and interface with external services (AWS, Azure, GCP, IBM Cloud).
* **Resources:** Define infrastructure objects (servers, storage, networks).
* **Terraform State:** Keeps track of infrastructure created by Terraform.

## 🚀 Why Use Terraform?

* Automates infrastructure provisioning.
* Ensures infrastructure consistency and reproducibility.
* Supports multiple cloud and service providers.
* Improves collaboration among team members.

## ⚙️ Essential Terraform Commands:

```bash
terraform init        # Initializes Terraform
terraform plan        # Previews changes Terraform will apply
terraform apply       # Creates or updates infrastructure
terraform destroy     # Removes Terraform-managed infrastructure
terraform version     # Checks installed Terraform version
```

## 🔐 AWS Credentials Setup:

To follow this course with real AWS infrastructure, you'll need to retrieve your AWS access keys.

👉 Read how to retrieve them here: How to Retrieve AWS Access Keys

📘 **Read how to retrieve them here:** [How to Retrieve AWS Access Keys](aws-access.md)

## 📌 Practical Example:

### Installing Terraform:

1. Download Terraform: [Official Download Link](https://developer.hashicorp.com/terraform/downloads)
2. Install Terraform and verify installation:

```bash
terraform --version
```

### Simple Terraform File Example (`main.tf`):

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-intro-example-bucket"
  acl    = "private"
}
```

## 🚧 Exercises:

* [Exercise 1: Terraform Installation and First Configuration](exercises/exercise-1.md)

## 🔗 References:

* [Terraform Documentation](https://developer.hashicorp.com/terraform/docs)
* [Infrastructure as Code Explained](https://www.hashicorp.com/resources/what-is-infrastructure-as-code)

---

Happy Learning! 🚀
