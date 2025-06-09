# Exercise 3: Your First Terraform Cloud Project

## Objectives

- Configure a cloud provider
- Create a simple web server infrastructure
- Understand resource dependencies
- Deploy and test your infrastructure

## Prerequisites

- AWS account (or another cloud provider of your choice)
- Configured credentials for your chosen provider

## Tasks

### 1. Provider Configuration

Create a new directory for your project with the following structure:

```
project/
├── main.tf       # Main configuration file
├── variables.tf   # Variable definitions
├── outputs.tf     # Output definitions
└── README.md      # Project documentation
```

In your `main.tf`, configure the AWS provider (or your chosen provider):

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = var.aws_region
}
```

In `variables.tf`, define your variables:

```hcl
variable "aws_region" {
  description = "AWS region to deploy resources"
  type        = string
  default     = "us-west-2"  # Change to your preferred region
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

variable "vpc_cidr" {
  description = "CIDR block for the VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "subnet_cidr" {
  description = "CIDR block for the subnet"
  type        = string
  default     = "10.0.1.0/24"
}
```

### 2. Create Basic Infrastructure

Add the following resources to your `main.tf`:

```hcl
# 1. VPC
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name = "project-vpc"
  }
}

# 2. Public Subnet
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = var.subnet_cidr
  map_public_ip_on_launch = true
  availability_zone       = "${var.aws_region}a"

  tags = {
    Name = "public-subnet"
  }
}

# 3. Internet Gateway
resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "main-igw"
  }
}

# 4. Route Table
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "public-rt"
  }
}

# 5. Route Table Association
resource "aws_route_table_association" "public" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public.id
}
```

### 3. Create Web Server Resources

Add web server resources to your `main.tf`:

```hcl
# 6. Security Group
resource "aws_security_group" "web" {
  name        = "web-sg"
  description = "Allow web and SSH traffic"
  vpc_id      = aws_vpc.main.id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
    description = "Allow HTTP"
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]  # In production, restrict to your IP
    description = "Allow SSH"
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    description = "Allow all outbound traffic"
  }

  tags = {
    Name = "web-sg"
  }
}

# 7. EC2 Instance with User Data
resource "aws_instance" "web" {
  ami                    = "ami-0c55b159cbfafe1f0"  # Update to a current AMI for your region
  instance_type          = var.instance_type
  subnet_id              = aws_subnet.public.id
  vpc_security_group_ids = [aws_security_group.web.id]
  
  # In a real project, use your own key pair or SSM Session Manager instead
  # key_name               = "your-key-pair"  

  user_data = <<-EOF
              #!/bin/bash
              yum update -y
              yum install -y httpd
              systemctl start httpd
              systemctl enable httpd
              echo "<h1>Hello from Terraform!</h1>" > /var/www/html/index.html
              echo "<h2>This server was deployed using Infrastructure as Code</h2>" >> /var/www/html/index.html
              EOF

  tags = {
    Name = "web-server"
  }
}
```

### 4. Define Outputs

In your `outputs.tf` file:

```hcl
output "vpc_id" {
  description = "ID of the created VPC"
  value       = aws_vpc.main.id
}

output "web_server_public_ip" {
  description = "Public IP address of the web server"
  value       = aws_instance.web.public_ip
}

output "web_url" {
  description = "URL of the web server"
  value       = "http://${aws_instance.web.public_ip}"
}
```

### 5. Deploy Your Infrastructure

Initialize, plan, and apply your configuration:

```bash
terraform init
terraform plan
terraform apply
```

### 6. Test Your Deployment

1. Wait a few minutes for the web server to initialize fully
2. Access your web server using the URL from the outputs
3. Verify that you can see the welcome page

### 7. Clean Up Resources

When you're done, destroy the resources to avoid unexpected charges:

```bash
terraform destroy
```

## Advanced Challenges

1. Modify your configuration to add a second web server in a different availability zone
2. Implement an Application Load Balancer to distribute traffic between the servers
3. Use a more secure method for SSH access, like allowing only your IP address

## Submission

Document your process, challenges faced, and include screenshots of your deployed resources and web page. Share your Terraform configuration files.
