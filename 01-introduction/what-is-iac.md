# What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is a practice of managing and provisioning computing infrastructure through machine-readable definition files rather than physical hardware configuration or interactive configuration tools. It treats infrastructure configuration as software code that can be stored, versioned, shared, and tested.

## Core Concepts of IaC

### Declarative vs. Imperative

- **Declarative**: Define the desired end state (what should be built), and the IaC tool determines how to achieve it
- **Imperative**: Define step-by-step instructions to achieve the end state (how to build it)

Terraform follows a primarily declarative approach, where you describe the desired infrastructure, and Terraform determines how to create, modify, or destroy resources to match that desired state.

### Idempotence

A key property of IaC tools is idempotence - the ability to run the same code multiple times and achieve the same result regardless of the starting state. This makes infrastructure deployments reliable and predictable.

### Version Control

IaC files can be stored in version control systems like Git, allowing for:
- History tracking of infrastructure changes
- Collaboration among team members
- Rollback to previous working states
- Code reviews for infrastructure changes

## Benefits of Using Terraform

### 1. Multi-Cloud Support

Terraform offers a consistent workflow across multiple providers and services. You can use the same tool and similar syntax to manage:
- Public clouds (AWS, Azure, GCP, etc.)
- Private clouds
- PaaS providers
- SaaS services

### 2. State Management

Terraform tracks the state of your infrastructure, creating a mapping between your configuration, the real-world resources, and resource dependencies. This allows Terraform to:
- Create and update complex infrastructures
- Avoid creating already existing resources
- Destroy resources when they are removed from the configuration

### 3. Resource Graph

Terraform builds a graph of all resources and parallelizes the creation and modification of independent resources, optimizing deployment speed.

### 4. Change Automation

- **Plan Phase**: Preview changes before applying them
- **Apply Phase**: Execute changes with proper dependency order
- **Destroy Phase**: Cleanly tear down infrastructure when needed

### 5. Modular Infrastructure

Terraform allows you to create reusable modules for common infrastructure patterns, promoting:
- Consistency across deployments
- Best practices
- Reduced duplication
- Simplified complex architectures

### 6. Community and Ecosystem

- Extensive provider ecosystem with thousands of resources supported
- Active community creating and sharing modules
- Rich plugin architecture
- Terraform Registry for discovering modules and providers

### 7. HCL (HashiCorp Configuration Language)

Terraform uses HCL which is:
- Human-readable and writable
- JSON-compatible
- Structured yet concise
- Easy to learn and use

### 8. Cost Control

- Preview changes before application helps prevent unexpected costs
- Ensures resources are created consistently
- Easy destruction of entire environments to avoid ongoing charges
- Resource tagging and management for billing purposes

### 9. Collaboration and Governance

- Team workflows through Terraform Cloud
- Policy as code through Sentinel
- Private module registry
- Role-based access control

### 10. Documentation as Code

The Terraform configuration itself serves as documentation for the infrastructure, showing:
- What resources exist
- How they're configured
- How they're connected
- What dependencies exist between components