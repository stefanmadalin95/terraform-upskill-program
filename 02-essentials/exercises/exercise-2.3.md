# 🧪 Exercise 2.3: Launching EC2 in a Custom VPC with Conditional Logic ☁️🖥️

## 🎯 Objective

Create a basic VPC and launch an EC2 instance inside it. Use a conditional variable to change instance type based on the environment.

## ✅ Tasks

1. Create a directory named `exercise-2.3`.
2. Inside that directory, create the following files:

### 📄 `variables.tf`

```hcl
variable "env" {
  description = "The environment type (dev or prod)."
  default     = "dev"
}

variable "region" {
  default = "us-east-1"
}
```

### 📄 `main.tf`

```hcl
provider "aws" {
  region = var.region
}

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "main" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.env == "prod" ? "t3.large" : "t3.micro"
  subnet_id     = aws_subnet.main.id

  tags = {
    Name = "example-${var.env}-instance"
  }
}
```

### 📄 `outputs.tf`

```hcl
output "instance_id" {
  value = aws_instance.example.id
}

output "vpc_id" {
  value = aws_vpc.main.id
}
```

## ▶️ Steps to Run

```bash
terraform init
terraform plan
terraform apply
```

🧼 When done, clean up with:

```bash
terraform destroy
```

---

💡 You just combined VPC, EC2, and conditional logic into a simple but powerful deployment!
