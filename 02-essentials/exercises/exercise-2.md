# Exercise 2: Terraform Essentials

## Objectives

- Work with variables and outputs
- Use expressions and functions
- Implement conditional logic
- Utilize meta-arguments

## Tasks

### 1. Variables and Outputs

Create a new directory and set up the following files:

**variables.tf**:
```hcl
variable "filename" {
  type        = string
  description = "The name of the file to create"
  default     = "example.txt"
}

variable "content" {
  type        = string
  description = "Content to write to the file"
  default     = "This is an example file."
}

variable "environment" {
  type        = string
  description = "Deployment environment"
  default     = "dev"
  validation {
    condition     = contains(["dev", "test", "prod"], var.environment)
    error_message = "Environment must be one of: dev, test, prod."
  }
}
```

**outputs.tf**:
```hcl
output "file_path" {
  value       = local_file.example.filename
  description = "Path to the created file"
}

output "file_content" {
  value       = local_file.example.content
  description = "Content of the created file"
  sensitive   = false
}
```

**main.tf**:
```hcl
terraform {
  required_providers {
    local = {
      source  = "hashicorp/local"
      version = "~> 2.0"
    }
  }
}

locals {
  env_prefix = {
    dev  = "development"
    test = "testing"
    prod = "production"
  }
  file_content = "Environment: ${lookup(local.env_prefix, var.environment)}\nContent: ${var.content}"
}

resource "local_file" "example" {
  content  = local.file_content
  filename = "${path.module}/${var.environment}_${var.filename}"
}
```

2. Run `terraform init`, `terraform plan`, and `terraform apply`
3. Try running with different variable values:
   ```bash
   terraform apply -var="environment=test" -var="content=Custom content"
   ```

### 2. Conditional Logic

Add the following to your main.tf:

```hcl
resource "local_file" "conditional_example" {
  content  = var.environment == "prod" ? "PRODUCTION WARNING: Sensitive data" : "Non-production environment"
  filename = "${path.module}/${var.environment}_warning.txt"
}
```

### 3. Meta-Arguments

Add the following to your main.tf:

```hcl
variable "file_count" {
  type    = number
  default = 3
}

variable "file_names" {
  type    = map(string)
  default = {
    "file1" = "First file content"
    "file2" = "Second file content"
    "file3" = "Third file content"
  }
}

# Using count
resource "local_file" "count_example" {
  count    = var.file_count
  content  = "This is file ${count.index + 1}"
  filename = "${path.module}/count_file_${count.index + 1}.txt"
}

# Using for_each
resource "local_file" "foreach_example" {
  for_each = var.file_names
  content  = each.value
  filename = "${path.module}/foreach_${each.key}.txt"
}
```

Run `terraform apply` and observe the created files.

## Submission

Share your terraform configuration files and document your observations about how variables, outputs, conditional logic, and meta-arguments work in Terraform.
