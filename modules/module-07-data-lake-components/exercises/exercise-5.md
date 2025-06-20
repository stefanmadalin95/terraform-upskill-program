# 🧪 Exercise 5: Create Glue Job to Query Catalog Data

## 🎯 Objective

Provision an AWS Glue job using Terraform that runs a Python script (stored in S3) to read data from the Glue Catalog. This simulates a basic data discovery or validation routine.

---

## 🧱 What You’ll Build

- A **Python script** stored in S3
- A **Glue Job** that references the script
- Linked IAM Role for Glue job execution
- Terraform configuration that wires it all together

---

## 🪜 Steps

### ✅ Step 1: Create the Python Script

Create a file named `read_glue_table.py` with the following content:

```python
import sys
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.job import Job

args = getResolvedOptions(sys.argv, ['JOB_NAME'])

sc = SparkContext()
glueContext = GlueContext(sc)
spark = glueContext.spark_session
job = Job(glueContext)
job.init(args['JOB_NAME'], args)

# Read table from Glue Catalog
dyf = glueContext.create_dynamic_frame.from_catalog(
    database="data_lake_metadata",
    table_name="raw_layer"
)

dyf.show()
job.commit()
```

💡 Upload this file to your S3 bucket, e.g.:
s3://<your-bucket-name>/glue-scripts/read_glue_table.py

### ✅ Step 2: Create the Terraform Module 

In modules/glue_python_job/:

#### `main.tf`

```hcl
resource "aws_glue_job" "this" {
  name     = var.job_name
  role_arn = var.iam_role_arn

  command {
    name            = "glueetl"
    script_location = var.script_location
    python_version  = "3"
  }

  glue_version        = "4.0"
  worker_type         = "G.1X"
  number_of_workers   = 2
  max_retries         = 0
  timeout             = 10
  tags                = var.tags
}
```

### ✅ Step 3: Define Variables and Outputs

#### `variables.tf`

```hcl
variable "job_name" {
  description = "Name of the Glue job"
  type        = string
}

variable "iam_role_arn" {
  description = "IAM Role ARN for the Glue job"
  type        = string
}

variable "script_location" {
  description = "S3 path to the Glue job script"
  type        = string
}

variable "tags" {
  description = "Tags to apply to the Glue job"
  type        = map(string)
}
```

#### `outputs.tf`

```hcl
output "glue_job_name" {
  value = aws_glue_job.this.name
}
```

### ✅ Step 4: Call the Module

In your root config:

```hcl
module "glue_python_job" {
  source          = "./modules/glue_python_job"
  job_name        = "read-raw-layer"
  iam_role_arn    = module.glue_iam_role.iam_role_arn
  script_location = "s3://${module.unique_bucket.bucket_name}/glue-scripts/read_glue_table.py"
  tags = {
    environment = "dev"
    owner       = "data-team"
    module      = "glue-job"
  }
}
```

### 🔁 Run the Workflow

```bash
terraform init
terraform plan
terraform apply
```

Then open the AWS Glue Console to manually start the job and monitor the output.

## 🧠 Reflection
- How would you expand this script to write to the curated layer?
- What validations could you build on top of this (e.g., schema checks)?
- What’s the advantage of keeping job scripts outside the Terraform repo?

---

➡️ **Back to Module:** [🧪 Module 07: Intro to Data Lake Components (Terraform + AWS)](../README.md)