# 🏗️ Module 08: Final Project — Build a Scalable Data Lake

## 🎯 Objective

Design and provision a fully automated AWS data lake infrastructure using Terraform that aligns with real-world ETL and data engineering best practices. This final project brings together everything you’ve learned in previous modules.

---

## 📦 What You’ll Build

An end-to-end data lake architecture that includes:

- S3 storage layers (raw, curated, processed)
- Glue metadata catalog
- Glue ETL job
- IAM roles and scoped permissions
- Athena integration for SQL querying
- Modular Terraform infrastructure

---

## ✅ Project Requirements

### 1. Infrastructure Provisioning

- Use Terraform 1.x
- All components must be deployed via code
- Use reusable modules from earlier exercises:
  - `s3_data_lake_bucket`
  - `glue_catalog_metadata`
  - `glue_python_job`
  - `iam_glue_data_access`
  - `athena_catalog`

---

### 2. Storage Layer (S3)

- Provision a uniquely named S3 bucket with these prefixes:
  - `/raw/` – landing zone for ingest
  - `/curated/` – cleaned/transformed output
  - `/processed/` – aggregated or final outputs
- Enable versioning and server-side encryption
- Apply consistent tagging for `environment`, `owner`, and `module`

---

### 3. Metadata Layer (Glue Catalog)

- Create a Glue Catalog Database: `data_lake_metadata`
- Define at least:
  - One table under the `raw/` prefix
  - One table under the `curated/` prefix
- Tables must include schema and SerDe details

---

### 4. Processing Layer (Glue Job)

- Create a Glue Job that:
  - Reads from the `raw_layer` Glue table
  - Performs a transformation (e.g. filter, rename column)
  - Writes data into the `curated/` path
- Script should be stored in S3 and referenced in Terraform
- IAM role must allow:
  - Read/write S3 for raw and curated
  - Glue catalog read/write

---

### 5. Query Layer (Athena)

- Create an Athena Database: `data_lake_queries`
- Configure a query result location in S3 (e.g., `/athena-results/`)
- Ensure Athena can read Glue tables and run sample queries manually

---

### 6. IAM and Security

- Create a scoped IAM role for Glue
  - Trust policy: `glue.amazonaws.com`
  - Permissions: no wildcards, only specific S3 ARNs and Glue actions
- Output the role ARN

---

### 7. Terraform Standards

- Use variables for all key values
- Use `terraform fmt`, `validate`, `plan`, and `apply`
- Define output values for key components (bucket, role, db, job, etc.)
- Use idempotent patterns — reapplying should not recreate unchanged infra

---

### 8. Constraints

- No hardcoded names — all resources must be parameterized
- Store all Terraform in version-controlled directories
- Use only official providers (AWS, random, etc.)
- No manual resource creation in the AWS Console

---

## 💡 Optional Enhancements (Advanced)

- Add S3 lifecycle rules for archival or expiration
- Partition data by source or ingestion date
- Add logging/monitoring on Glue Jobs
- Create staging and prod environments using Terraform workspaces

---

## 🧠 Deliverables

- Terraform codebase with clear module usage
- Sample Python script for the Glue job
- Outputs displayed after `terraform apply`
- Manual test results for Athena queries

---

🎓 Congratulations! This project validates your ability to apply infrastructure-as-code and data lake principles in a practical and modular way.