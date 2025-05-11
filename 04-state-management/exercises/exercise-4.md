# Exercise 4: Terraform State Management

## Objectives

- Configure a remote state backend
- Work with state operations
- Use Terraform workspaces

## Prerequisites

- Access to a cloud provider (AWS/Azure/GCP)
- Basic infrastructure created from previous exercises

## Tasks

### 1. Configure a Remote State Backend

#### For AWS

1. Create an S3 bucket for remote state:

```hcl
# backend.tf
provider "aws" {
  region = "us-west-2"  # Change to your region
}

# Create an S3 bucket to store the state file
resource "aws_s3_bucket" "terraform_state" {
  bucket = "your-unique-tf-state-bucket"  # Must be globally unique

  # Prevent accidental deletion of this S3 bucket
  lifecycle {
    prevent_destroy = true
  }
}

# Enable versioning for the S3 bucket
resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.terraform_state.id
  versioning_configuration {
    status = "Enabled"
  }
}

# Create a DynamoDB table for state locking
resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-state-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

2. Apply this configuration to create the resources:

```bash
terraform init
terraform apply
```

3. Update your configuration to use the remote backend:

```hcl
# main.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }

  backend "s3" {
    bucket         = "your-unique-tf-state-bucket"  # Same as above
    key            = "terraform.tfstate"
    region         = "us-west-2"  # Change to your region
    dynamodb_table = "terraform-state-locks"
    encrypt        = true
  }
}
```

4. Reinitialize Terraform to migrate the state:

```bash
terraform init -migrate-state
```

### 2. Work with State Operations

Try the following state operations:

1. List resources in the state:

```bash
terraform state list
```

2. Show details of a specific resource:

```bash
terraform state show aws_instance.web
```

3. Remove a resource from state (will NOT destroy the actual resource):

```bash
terraform state rm aws_security_group.web
```

4. Import the resource back:

```bash
terraform import aws_security_group.web <security-group-id>
```

### 3. Use Terraform Workspaces

1. Create and use workspaces for different environments:

```bash
terraform workspace new dev
terraform workspace new staging
terraform workspace new prod
```

2. Modify your configuration to be workspace-aware:

```hcl
# variables.tf
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

# main.tf
locals {
  workspace_env = {
    dev     = "development"
    staging = "staging"
    prod    = "production"
  }

  env = lookup(local.workspace_env, terraform.workspace, "development")
  
  instance_type = {
    dev     = "t2.micro"
    staging = "t2.small"
    prod    = "t2.medium"
  }
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"  # Update to current AMI
  instance_type = lookup(local.instance_type, terraform.workspace, var.instance_type)
  
  tags = {
    Name        = "web-server-${local.env}"
    Environment = local.env
  }
  
  # Other configuration as needed
}
```

3. Switch between workspaces and apply:

```bash
terraform workspace select dev
terraform apply

terraform workspace select staging
terraform apply

terraform workspace select prod
terraform apply
```

### 4. View State in Remote Backend

Check your remote backend (S3 bucket or equivalent) to see how Terraform stores state for different workspaces.

## Advanced Challenges

1. Set up Terraform Cloud as a backend instead of S3.
2. Create a script that performs a state backup before applying changes.
3. Implement a CI/CD pipeline that uses Terraform workspaces for different environments.

## Submission

Document your experience with remote state, state operations, and workspaces. Include screenshots of your backend configuration and how states differ between workspaces.
