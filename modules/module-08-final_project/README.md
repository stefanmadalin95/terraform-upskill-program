# 🏗️ Module 08: Final Project — Build a Scalable Data Lake

## 🎯 Objective

Design and provision a fully automated AWS data lake infrastructure using Terraform that aligns with real-world ETL and data engineering best practices. This final project brings together everything you’ve learned in previous modules.

---

## 📦 What You’ll Build

An end-to-end data lake architecture that includes:

- S3 storage Layer (raw, processed)
- Glue metadata catalog
- Glue ETL job
- IAM roles and scoped permissions
- Athena integration for SQL querying
- Modular Terraform infrastructure

---

## 🔗 References

Explore deeper all resources needed to implement this project in [references](references.md).

---


## 📚 Project Requirements

### ✅ General Requirements

- Terraform Version: Use Terraform version >= 1.0.0, < 2.0.0.
- AWS Provider: Use AWS provider version ~> 4.0.

### ✅ Infrastructure Requirements

#### 1️⃣ S3 Bucket:

- Create an S3 bucket for the data lake with logical prefixes:  
  - 📁 raw/  
  - 📁 processed/  
  - 📁 scripts/  
  - 📁 athena-results/  

- Enable versioning and server-side encryption (AES256).
- Apply consistent tags to all resources.

#### 2️⃣ Glue Catalog:

- Create a Glue database named data_lake_metadata.
- Define two tables:
  - raw_data (CSV format).
  - processed_data (Parquet format).
- Ensure schemas match the data format.


#### 3️⃣ Glue Job:

- Create a Glue job named data-lake-transformation-job:
- Use Python 3.9 and Glue version 3.0.
- Perform transformations:
  - Add a processed_date column.
  - Filter out rows with null values.
- Write output to the `processed/` folder in Parquet format.
- Partition data by processed_date.

#### 4️⃣ Athena:

- Create an Athena workgroup named data-lake-workgroup.
- Configure query results to be stored in /athena-results/.
- Define a named query to query the processed_data table.

#### 5️⃣ IAM Roles and Policies:

- Create an IAM role for Glue with:
  - Permissions to access the S3 bucket prefixes (raw, processed, scripts).
  - Permissions to interact with the Glue Catalog.
- Attach the AWSGlueServiceRole managed policy.


### ✅ Data Requirements

- Sample Data:
  - Provide a sample CSV file (sample_data.csv) for testing.
  - Ensure the file contains columns: id, name, timestamp, value.

### ✅ Tagging Requirements

- Apply consistent tags across all resources:
  - `Environment`: dev
  - `Project`: ibm-data-lake
  - `ManagedBy`: terraform
- Additional tags can be customized in terraform.tfvars.


### ✅ Testing Requirements

- Upload Sample Data:
  - Upload the sample data to the /raw/ prefix in the S3 bucket.
- Run Glue Job:
  - Trigger the Glue job manually or via automation.
- Query Data:
  - Use Athena to query the processed_data table.
- Validate partitioning by processed_date.

### ✅ Security Requirements

- Encryption:
  - Enable server-side encryption for S3 bucket objects.
  - Use SSE-S3 for Athena query results.

- IAM Policies:
  - Restrict permissions to specific S3 prefixes and Glue resources.

### ✅ Modular Design Requirements

Use Terraform modules for:
- S3 bucket (s3).
- IAM roles and policies (iam).
- Glue resources (glue).
- Athena resources (athena).

### ✅ Deployment Requirements

Terraform Workflow:

- Initialize Terraform (terraform init).
- Validate configuration (terraform validate).
- Format code (terraform fmt).
- Preview changes (terraform plan).
- Apply changes (terraform apply).

### ✅ Clean-Up:
- After testing has been performed, destroy all resources using terraform destroy to avoid additional costs.

---

#### 🎓 Congratulations! This project validates your ability to apply infrastructure-as-code and data lake principles in a practical and modular way.