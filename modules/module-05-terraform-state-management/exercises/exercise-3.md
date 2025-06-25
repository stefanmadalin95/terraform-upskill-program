# 📝 Exercise 3: Add DynamoDB Locking (Optional)

## Objective

Prevent team members from applying changes to the same state file at the same time. This avoids conflicts and corrupted state by enabling Terraform's built-in state locking using DynamoDB.

---

## Steps

✅ Use the existing DynamoDB table

The locking table has already been created by the course owner.  
Name: terraform-state-locks  
📌 This table uses the LockID as the primary key and is shared by all engineers.  

✅ Update your `backend.tf` to enable locking:

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-state-files-759505726502" # Shared bucket
    key            = "stefan/terraform.tfstate"           # Change to your folder
    region         = "eu-west-1"
    dynamodb_table = "terraform-state-locks"
  }
}
```

✅ Re-run:

```bash
terraform init
terraform plan
terraform apply
```

✅ Inspect the Lock in DynamoDB

- Go to the AWS Console → DynamoDB → Tables → terraform-state-locks
- Select the Items tab
- Start a terraform apply in one terminal  
🔍 You will see a new item created with:  
    - LockID: matches your key in backend.tf (e.g., stefan/terraform.tfstate)
    - Lock metadata like CreatedTime, Info, and Operation
    - Cancel or let the apply finish and see the lock disappear
    - This is how Terraform enforces exclusive apply rights—by writing a lock record in DynamoDB.

## Reflection
- Why is locking important in a CI/CD pipeline?
- Have you ever seen inconsistent environments due to parallel changes?

---

➡️ **Next Exercise:** [🧪 Exercise 4: Simulate a Mini Project Setup](./exercise-4.md)