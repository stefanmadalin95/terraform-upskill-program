# Module 02: Terraform Essentials 🧱

## 📖 Learning Objectives:

By the end of this module, you should be able to:

* ✍️ Write simple Terraform configurations.
* 🔄 Use variables and outputs to make your code flexible.
* 🔢 Use basic expressions and functions.
* ❓ Add simple if-else logic (conditional logic).
* 🧮 Create multiple resources using loops.

---

## 📚 Topics Covered

### 1. 🧾 HCL Syntax (HashiCorp Configuration Language)

Terraform uses a special syntax called HCL, which looks a bit like JSON but is easier to read and write.

* Code is written in blocks like `resource`, `variable`, or `output`.
* Inside blocks, you define settings with key = value pairs.

### 2. 📁 Terraform Files

* `.tf` – Your main configuration files.
* `.tfvars` – Files that store variable values.
* `terraform.tfstate` – Keeps track of what Terraform has created.

### 3. ⚙️ Resources and Data Sources

* **Resources**: Things you want to create, like EC2 instances or S3 buckets.
* **Data Sources**: Info you want to read from AWS, but not create.

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}
```

### 4. 🧩 Variables and Outputs

Use **variables** so you can change settings without editing all your code.

```hcl
variable "region" {
  default = "us-east-1"
}
```

Use **outputs** to show values after your infrastructure is created.

```hcl
output "instance_ip" {
  value = aws_instance.example.public_ip
}
```

### 5. 🧠 Expressions and Functions

Functions help you do things like change text or count items.

```hcl
locals {
  name = upper("dev-instance")
}
```

### 6. ❓ Conditional Logic

Use if-else style logic with `? :`

```hcl
instance_type = var.env == "prod" ? "t3.large" : "t3.micro"
```

### 7. 🔁 Meta-Arguments: `count` and `for_each`

Create multiple resources with `count`:

```hcl
resource "aws_instance" "example" {
  count         = 2
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

Or use `for_each` to loop over names:

```hcl
resource "aws_s3_bucket" "example" {
  for_each = toset(["logs", "images"])
  bucket   = "my-${each.key}-bucket"
  acl      = "private"
}
```

---

## 🧪 Exercises:

📝 Try these hands-on tasks to practice:

* [Exercise 2.1: Using Variables and Outputs](exercises/exercise-2.1.md)
* [Exercise 2.2: Creating Multiple Resources](exercises/exercise-2.2.md)
* [Exercise 2.3: Simple Logic and Functions](exercises/exercise-2.3.md)

---

## 🔗 References:

* [Terraform Language Docs](https://developer.hashicorp.com/terraform/language)
* [Terraform Functions](https://developer.hashicorp.com/terraform/language/functions)

---

Keep it simple, practice often, and you’ll be building infrastructure with ease! 💪
