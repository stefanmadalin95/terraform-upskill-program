# Terraform Cheat Sheet

## Basic Commands

```bash
# Initialize a Terraform configuration
terraform init

# Preview changes
terraform plan

# Apply changes
terraform apply

# Apply without asking for approval
terraform apply -auto-approve

# Destroy resources
terraform destroy

# Validate configuration files
terraform validate

# Format configuration files
terraform fmt
```

## Working with Variables

```bash
# Apply with a variable file
terraform apply -var-file="prod.tfvars"

# Apply with individual variables
terraform apply -var="region=us-west-2" -var="instance_type=t2.micro"

# Apply with environment variables
# TF_VAR_variable_name format
TF_VAR_region=us-west-2 terraform apply
```

## State Management

```bash
# List resources in state
terraform state list

# Show state for a specific resource
terraform state show aws_instance.web

# Move a resource within state
terraform state mv aws_instance.old aws_instance.new

# Remove a resource from state
terraform state rm aws_instance.web

# Pull current state
terraform state pull

# Push state
terraform state push

# Import existing infrastructure into state
terraform import aws_instance.web i-1234567890abcdef0
```

## Workspaces

```bash
# List workspaces
terraform workspace list

# Create a new workspace
terraform workspace new dev

# Select a workspace
terraform workspace select prod

# Delete a workspace
terraform workspace delete dev

# Show current workspace
terraform workspace show
```

## Output Management

```bash
# Show all outputs
terraform output

# Show specific output
terraform output vpc_id

# Show output in JSON format
terraform output -json
```

## Module Management

```bash
# Get modules
terraform get

# Update modules
terraform get -update
```

## Other Useful Commands

```bash
# Generate a graph of the resources
terraform graph

# Show provider information
terraform providers

# Initialize and upgrade modules/plugins
terraform init -upgrade

# Terraform console for expression testing
terraform console
```

## Common HCL Syntax

### Resource Block
```hcl
resource "aws_instance" "web" {
  ami           = "ami-a1b2c3d4"
  instance_type = "t2.micro"
  tags = {
    Name = "web-server"
  }
}
```

### Data Source Block
```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}
```

### Variable Declaration
```hcl
variable "instance_type" {
  description = "Type of EC2 instance"
  type        = string
  default     = "t2.micro"
}
```

### Output Declaration
```hcl
output "instance_ip" {
  description = "Public IP of the instance"
  value       = aws_instance.web.public_ip
}
```

### Module Usage
```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "3.14.0"
  
  name = "my-vpc"
  cidr = "10.0.0.0/16"
}
```

### Local Values
```hcl
locals {
  common_tags = {
    Environment = "production"
    Project     = "web-app"
  }
}
```

### Conditional Expression
```hcl
resource "aws_instance" "web" {
  instance_type = var.environment == "prod" ? "t2.medium" : "t2.micro"
}
```

### Count Meta-Argument
```hcl
resource "aws_instance" "server" {
  count = 3
  ami   = "ami-a1b2c3d4"
  tags  = {
    Name = "server-${count.index}"
  }
}
```

### For_each Meta-Argument
```hcl
resource "aws_s3_bucket" "data" {
  for_each = toset(["logs", "reports", "data"])
  bucket   = "${each.key}-bucket"
}
```

## Remote State Configuration

### AWS S3 Backend
```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "path/to/my/key"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

### Azure Storage Backend
```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "StorageAccount-ResourceGroup"
    storage_account_name = "terraformstate"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```

### Google Cloud Storage Backend
```hcl
terraform {
  backend "gcs" {
    bucket = "terraform-state-bucket"
    prefix = "terraform/state"
  }
}
```
