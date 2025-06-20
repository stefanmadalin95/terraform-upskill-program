# 🔎 Exercise 3: Connect Athena to Glue Catalog

## 🎯 Objective

Create an Athena database that reads metadata from your Glue Catalog. This allows querying your data lake using SQL directly in Athena.

---

## 🧱 What You’ll Build

- An **Athena database** linked to your Glue Catalog
- A dedicated **S3 bucket or prefix** to store query results

---

## 🪜 Steps

### ✅ Step 1: Create a New Module

Create a new module called `athena_catalog/`.

#### `main.tf`

```hcl
resource "aws_athena_database" "this" {
  name   = var.athena_db_name
  bucket = var.query_result_location
}
```
💡 This creates an Athena logical database that references your Glue catalog automatically under the hood.

### ✅ Step 2: Define Variables and Outputs

#### `variables.tf`

```hcl
variable "athena_db_name" {
  description = "Name of the Athena database"
  type        = string
}

variable "query_result_location" {
  description = "S3 bucket/prefix where Athena will store results"
  type        = string
}
```

### `outputs.tf`

```hcl
output "athena_db_name" {
  value = aws_athena_database.this.name
}
```

### ✅ Step 3: Call the Module

In your root configuration:

```hcl
module "athena_catalog" {
  source                = "./modules/athena_catalog"
  athena_db_name        = "data_lake_queries"
  query_result_location = "s3://${module.unique_bucket.bucket_name}/athena-results/"
}
```

### 🔁 Run the Workflow

```bash
terraform init
terraform plan
terraform apply
```

### ✅ Manual Validation

After applying:
- Go to the Athena Console.
- Select the data_lake_queries database.
- Run a query like:

```sql
SELECT * FROM raw_layer LIMIT 10;
```

🔁 If you don’t see tables, check if the Glue table was created correctly and the S3 location contains readable data.

## 🧠 Reflection
- How does Athena leverage the Glue catalog for its operations?
- Why is a result location needed for queries?
- How could you automate table discovery or crawling in future?

---

➡️ **Next Exercise:** [🧪 Exercise 4: Create IAM Role for Catalog Access](./exercise-4.md)