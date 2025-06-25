# 📝 Exercise 2: Set Up Remote Backend in S3

## Objective

Configure your Terraform project to use a remote S3 backend for storing state. This setup is designed to support team collaboration, using folders for each data engineer and a shared bucket created by the course owner.

---

## Prerequisites

The S3 bucket has already been created by the course owner.
Name format: terraform-state-files-<AWS_ACCOUNT_ID>  
✅ Example: terraform-state-files-759505726502

Each engineer will store their state in a personal folder inside this bucket.

## Steps

✅ Create a new file `backend.tf` with this content:

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state-files-759505726502"
    key    = "stefan/terraform.tfstate"           # Replace 'stefan' with your folder
    region = "eu-west-1"
  }
}
```

✅ Reinitialize your project:

```bash
terraform init
terraform plan
terraform apply
```

✅ Verify the message that state is being moved

## Reflection
- What are the advantages of using S3 for state?
-How would this support a team working together?

---

➡️ **Next Exercise:** [🧪 Exercise 3: Add DynamoDB Locking (Optional)](./exercise-3.md)