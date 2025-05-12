# Terraform Essentials: Exercises for Module 2

## 🧪 Exercise 2.1: Working with Variables and Outputs

### Objective:

Create a Terraform configuration that uses input variables and outputs resource attributes.

### Tasks:

1. Define a variable for the AWS region and instance type.
2. Use these variables in an `aws_instance` resource.
3. Output the instance ID and public IP address after the infrastructure is applied.

### Example:

* `variables.tf`

```hcl
variable "region" {
  default = "us-east-1"
}

variable "instance_type" {
  default = "t2.micro"
}
```

* `main.tf`

```hcl
provider "aws" {
  region = var.region
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_type
}
```

* `outputs.tf`

```hcl
output "instance_id" {
  value = aws_instance.example.id
}

output "public_ip" {
  value = aws_instance.example.public_ip
}
```

---

## 🧪 Exercise 2.2: Creating Resources with Meta-Arguments

### Objective:

Use `count` and `for_each` to dynamically create multiple resources.

### Tasks:

1. Create 3 EC2 instances using the `count` meta-argument.
2. Create 2 S3 buckets using `for_each` and a list of names.

### Example:

* EC2 Instances with `count`:

```hcl
resource "aws_instance" "multi" {
  count         = 3
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "Instance-${count.index}"
  }
}
```

* S3 Buckets with `for_each`:

```hcl
variable "bucket_names" {
  default = ["app-logs", "app-images"]
}

resource "aws_s3_bucket" "buckets" {
  for_each = toset(var.bucket_names)

  bucket = "my-${each.key}-bucket"
  acl    = "private"
}
```

---

## 🧪 Exercise 2.3: Using Functions and Conditional Logic

### Objective:

Use Terraform expressions, functions, and conditional logic.

### Tasks:

1. Use the `upper()` function to transform a tag name to uppercase.
2. Use conditional logic to assign different instance types based on the environment.

### Example:

```hcl
variable "env" {
  default = "dev"
}

resource "aws_instance" "env_based" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.env == "prod" ? "t3.large" : "t3.micro"
  tags = {
    Environment = upper(var.env)
  }
}
```

---

✅ **Next Step:** Run `terraform init`, `plan`, and `apply` for each of the above configurations and observe the changes.

📁 Don’t forget to clean up with `terraform destroy` after you complete each exercise.
