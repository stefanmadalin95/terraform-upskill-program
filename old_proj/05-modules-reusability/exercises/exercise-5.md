# Exercise 5: Terraform Modules and Reusability

## Objectives

- Create a custom Terraform module
- Use the module in a project
- Implement versioning and best practices
- Use public modules from the Terraform Registry

## Tasks

### 1. Create a Basic Module

Create a module directory structure for a reusable VPC module:

```
modules/
├── vpc/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    └── README.md
```

In the `vpc` module, create the following files:

**variables.tf**:
```hcl
variable "vpc_name" {
  description = "Name of the VPC"
  type        = string
}

variable "vpc_cidr" {
  description = "CIDR block for the VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "azs" {
  description = "Availability zones to use"
  type        = list(string)
  default     = ["us-west-2a", "us-west-2b"]  # Update for your region
}

variable "public_subnet_cidrs" {
  description = "CIDR blocks for public subnets"
  type        = list(string)
  default     = ["10.0.1.0/24", "10.0.2.0/24"]
}

variable "private_subnet_cidrs" {
  description = "CIDR blocks for private subnets"
  type        = list(string)
  default     = ["10.0.11.0/24", "10.0.12.0/24"]
}

variable "enable_nat_gateway" {
  description = "Enable NAT Gateway for private subnets"
  type        = bool
  default     = true
}

variable "tags" {
  description = "Tags to apply to resources"
  type        = map(string)
  default     = {}
}
```

**main.tf**:
```hcl
resource "aws_vpc" "this" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = merge(
    {
      "Name" = var.vpc_name
    },
    var.tags
  )
}

# Public subnets
resource "aws_subnet" "public" {
  count = length(var.public_subnet_cidrs)

  vpc_id                  = aws_vpc.this.id
  cidr_block              = var.public_subnet_cidrs[count.index]
  availability_zone       = var.azs[count.index % length(var.azs)]
  map_public_ip_on_launch = true

  tags = merge(
    {
      "Name" = "${var.vpc_name}-public-${count.index + 1}"
    },
    var.tags
  )
}

# Private subnets
resource "aws_subnet" "private" {
  count = length(var.private_subnet_cidrs)

  vpc_id            = aws_vpc.this.id
  cidr_block        = var.private_subnet_cidrs[count.index]
  availability_zone = var.azs[count.index % length(var.azs)]

  tags = merge(
    {
      "Name" = "${var.vpc_name}-private-${count.index + 1}"
    },
    var.tags
  )
}

# Internet Gateway
resource "aws_internet_gateway" "this" {
  vpc_id = aws_vpc.this.id

  tags = merge(
    {
      "Name" = "${var.vpc_name}-igw"
    },
    var.tags
  )
}

# Route Tables
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.this.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.this.id
  }

  tags = merge(
    {
      "Name" = "${var.vpc_name}-public-rt"
    },
    var.tags
  )
}

resource "aws_route_table_association" "public" {
  count = length(var.public_subnet_cidrs)

  subnet_id      = aws_subnet.public[count.index].id
  route_table_id = aws_route_table.public.id
}

# NAT Gateway (optional)
resource "aws_eip" "nat" {
  count = var.enable_nat_gateway ? 1 : 0
  domain = "vpc"

  tags = merge(
    {
      "Name" = "${var.vpc_name}-nat-eip"
    },
    var.tags
  )
}

resource "aws_nat_gateway" "this" {
  count = var.enable_nat_gateway ? 1 : 0

  allocation_id = aws_eip.nat[0].id
  subnet_id     = aws_subnet.public[0].id

  tags = merge(
    {
      "Name" = "${var.vpc_name}-nat"
    },
    var.tags
  )

  depends_on = [aws_internet_gateway.this]
}

resource "aws_route_table" "private" {
  count = var.enable_nat_gateway ? 1 : 0

  vpc_id = aws_vpc.this.id

  route {
    cidr_block     = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.this[0].id
  }

  tags = merge(
    {
      "Name" = "${var.vpc_name}-private-rt"
    },
    var.tags
  )
}

resource "aws_route_table_association" "private" {
  count = var.enable_nat_gateway ? length(var.private_subnet_cidrs) : 0

  subnet_id      = aws_subnet.private[count.index].id
  route_table_id = aws_route_table.private[0].id
}
```

**outputs.tf**:
```hcl
output "vpc_id" {
  description = "The ID of the VPC"
  value       = aws_vpc.this.id
}

output "vpc_cidr" {
  description = "The CIDR block of the VPC"
  value       = aws_vpc.this.cidr_block
}

output "public_subnet_ids" {
  description = "List of public subnet IDs"
  value       = aws_subnet.public.*.id
}

output "private_subnet_ids" {
  description = "List of private subnet IDs"
  value       = aws_subnet.private.*.id
}

output "nat_gateway_ids" {
  description = "List of NAT Gateway IDs"
  value       = aws_nat_gateway.this.*.id
}

output "internet_gateway_id" {
  description = "ID of the Internet Gateway"
  value       = aws_internet_gateway.this.id
}
```

**README.md**:
```markdown
# AWS VPC Terraform Module

This module creates a VPC with the following components:

- VPC with CIDR block
- Public and private subnets across multiple availability zones
- Internet Gateway
- NAT Gateway (optional)
- Route tables for public and private subnets

## Usage

```hcl
module "vpc" {
  source = "./modules/vpc"

  vpc_name = "my-vpc"
  vpc_cidr = "10.0.0.0/16"
  
  # Add other variables as needed
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|------------|------|---------|:--------:|
| vpc_name | Name of the VPC | `string` | n/a | yes |
| vpc_cidr | CIDR block for the VPC | `string` | `"10.0.0.0/16"` | no |
| azs | Availability zones to use | `list(string)` | `["us-west-2a", "us-west-2b"]` | no |
| public_subnet_cidrs | CIDR blocks for public subnets | `list(string)` | `["10.0.1.0/24", "10.0.2.0/24"]` | no |
| private_subnet_cidrs | CIDR blocks for private subnets | `list(string)` | `["10.0.11.0/24", "10.0.12.0/24"]` | no |
| enable_nat_gateway | Enable NAT Gateway for private subnets | `bool` | `true` | no |
| tags | Tags to apply to resources | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| vpc_id | The ID of the VPC |
| vpc_cidr | The CIDR block of the VPC |
| public_subnet_ids | List of public subnet IDs |
| private_subnet_ids | List of private subnet IDs |
| nat_gateway_ids | List of NAT Gateway IDs |
| internet_gateway_id | ID of the Internet Gateway |
```

### 2. Create a Project Using Your Module

Create a new directory for your project with the following structure:

```
project/
├── main.tf
├── variables.tf
├── outputs.tf
└── backend.tf (optional)
```

In your project's `main.tf`, use your module:

```hcl
provider "aws" {
  region = var.aws_region
}

module "vpc" {
  source = "../modules/vpc"

  vpc_name = "${var.environment}-vpc"
  vpc_cidr = var.vpc_cidr
  azs      = var.availability_zones

  tags = {
    Environment = var.environment
    Project     = "module-demo"
    ManagedBy   = "terraform"
  }
}

# Create a security group using the VPC module output
resource "aws_security_group" "example" {
  name        = "${var.environment}-example-sg"
  description = "Example security group"
  vpc_id      = module.vpc.vpc_id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Environment = var.environment
    ManagedBy   = "terraform"
  }
}
```

In your `variables.tf`:

```hcl
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-west-2"
}

variable "environment" {
  description = "Environment name"
  type        = string
  default     = "dev"
}

variable "vpc_cidr" {
  description = "VPC CIDR block"
  type        = string
  default     = "10.0.0.0/16"
}

variable "availability_zones" {
  description = "List of availability zones"
  type        = list(string)
  default     = ["us-west-2a", "us-west-2b"]
}
```

In your `outputs.tf`:

```hcl
output "vpc_id" {
  description = "The ID of the VPC"
  value       = module.vpc.vpc_id
}

output "public_subnet_ids" {
  description = "The IDs of the public subnets"
  value       = module.vpc.public_subnet_ids
}

output "private_subnet_ids" {
  description = "The IDs of the private subnets"
  value       = module.vpc.private_subnet_ids
}
```

### 3. Use a Module from the Terraform Registry

In your project, add a module from the Terraform Registry:

```hcl
# Add to your project main.tf
module "s3_bucket" {
  source  = "terraform-aws-modules/s3-bucket/aws"
  version = "3.7.0"

  bucket = "${var.environment}-demo-bucket"
  acl    = "private"

  versioning = {
    enabled = true
  }

  tags = {
    Environment = var.environment
    ManagedBy   = "terraform"
  }
}
```

### 4. Deploy Your Project

Initialize and apply your configuration:

```bash
terraform init
terraform plan
terraform apply
```

### 5. Module Versioning

If you're working in a team or planning to share your module, create a Git repository for it and use version tags.

Simple versioning workflow:

1. Initialize a Git repository in your module directory:
   ```bash
   cd modules/vpc
   git init
   git add .
   git commit -m "Initial module version"
   ```

2. Add a tag for version 1.0.0:
   ```bash
   git tag v1.0.0
   ```

3. Update your project to reference a specific version:
   ```hcl
   module "vpc" {
     source = "git::https://github.com/yourusername/terraform-aws-vpc.git?ref=v1.0.0"
     
     vpc_name = "${var.environment}-vpc"
     # Other variables...
   }
   ```

## Advanced Challenges

1. Create a module for a complete application stack (VPC, EC2, RDS, etc.)
2. Publish your module to the Terraform Registry (requires GitHub)
3. Implement a more complex module that supports multiple deployment scenarios

## Submission

Share your module code and project configuration. Document the following:

1. Module structure and design decisions
2. How you've implemented versioning
3. Explain how your module improves reusability
4. Screenshots of deployed infrastructure
