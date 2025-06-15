# 📝 Exercise 2: Set Up Remote Backend in S3

## Objective

Move your Terraform state to an S3 bucket.

---

## Steps

✅ Create an S3 bucket (manually or with Terraform)  
✅ Create a new file `backend.tf` with this content:

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state-yourname"
    key    = "terraform.tfstate"
    region = "eu-west-1"
  }
}
```

✅ Reinitialize your project:

```bash
terraform init
```

✅ Verify the message that state is being moved

## Reflection
- What are the advantages of using S3 for state?
-How would this support a team working together?

