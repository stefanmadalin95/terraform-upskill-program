# Module 02: Terraform Essentials 🧱

## 📖 Learning Objectives:

By the end of this module, you should be able to:

* Write Terraform configurations using HCL syntax.
* Define and use variables and outputs.
* Utilize expressions and built-in functions.
* Implement conditional logic in your configurations.
* Use meta-arguments (like `count` and `for_each`) to dynamically manage resources.

## 📚 Topics Covered:

### 1. HCL (HashiCorp Configuration Language) Syntax

* Terraform uses HCL, a declarative configuration language designed for readability.
* Syntax consists of blocks (e.g., `resource`, `variable`, `output`), arguments, and expressions.

### 2. Terraform File Structure

* `.tf` files: Main configuration files.
* `.tfvars`: Variables file used to pass values.
* `terraform.tfstate`: Tracks the state of infrastructure.

### 3. Resources and Data Sources

* **Resources:** Core building blocks (e.g., `aws_instance`, `azurerm_storage_account`).
* **Data Sources:** Read-only views into existing infrastructure managed outside Terraform.

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}
```

### 4. Variables and Outputs

* **Variables** allow parameterization of configurations.

```hcl
variable "region" {
  description = "The AWS region to use."
  type        = string
  default     = "us-east-1"
}
```

* **Outputs** are used to expose values after `apply`.

```hcl
output "instance_ip" {
  value = aws_instance.example.public_ip
}
```

### 5. Expressions and Functions

* Expressions compute or transform values.
* Built-in functions like `join`, `length`, `lookup`, `file`, `element`, etc.

```hcl
locals {
  name = upper("dev-instance")
}
```

### 6. Conditional Logic

* Ternary operator syntax: `condition ? true_value : false_value`

```hcl
resource "aws_instance" "example" {
  instance_type = var.env == "prod" ? "t3.large" : "t3.micro"
  ami           = "ami-123456"
}
```

### 7. Meta-Arguments

* **`count`**: Create multiple instances of a resource.

```hcl
resource "aws_instance" "example" {
  count         = 3
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

* **`for_each`**: Iterate over maps or sets of strings.

```hcl
resource "aws_s3_bucket" "example" {
  for_each = toset(["logs", "images"])
  bucket   = "my-${each.key}-bucket"
  acl      = "private"
}
```

## 🧪 Exercises:

> The `exercises/` directory contains hands-on activities for the following:

* [Exercise 2.1: Working with Variables and Outputs](exercises/exercise-2.1.md)
* [Exercise 2.2: Creating Resources with Meta-Arguments](exercises/exercise-2.2.md)
* [Exercise 2.3: Using Functions and Conditional Logic](exercises/exercise-2.3.md)

## 🔗 References:

* [Terraform Language Documentation](https://developer.hashicorp.com/terraform/language)
* [Terraform Functions Reference](https://developer.hashicorp.com/terraform/language/functions)

---

Mastering these essentials builds the foundation for more advanced Terraform use. Keep practicing! 💪
