# 📝 Exercise 2: Create Multiple Resources

## Objective

Add multiple resources to see how Terraform can manage them together.

---

## Steps

✅ Create a file called `main.tf`.

✅ In `main.tf`, add:

```hcl
resource "aws_s3_bucket" "data_bucket" {
  bucket = "my-first-data-lake-bucket"
}
```

✅ Now, let’s add another resource: an IAM Role for data processing jobs.

```hcl
resource "aws_iam_role" "data_role" {
  name = "data-processing-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Action = "sts:AssumeRole",
      Effect = "Allow",
      Principal = {
        Service = "ec2.amazonaws.com"
      }
    }]
  })
}
```

✅ Run:

```bash
terraform plan
```

✅ Apply the changes:

```bash
terraform apply
```

✅ Verify that both the bucket and the IAM Role were created in your AWS console.

## Reflection
- How does Terraform handle creating multiple resources together?
- How would you describe the advantage of defining these resources in code rather than clicking in the console?

---

➡️ **Next Exercise:** [🧪 Exercise 3: Add Variables for Flexibility](./exercise-3.md)