# 📚 Module 08 References

Here are some helpful resources for putting it all together:


## 🪣 S3 Bucket

| Requirement                     | Terraform Resource                     | Documentation Link                                                                                                                       |
| ------------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Create bucket with prefixes     | `aws_s3_bucket` + `aws_s3_object`      | [aws\_s3\_bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)                                 |
| Logical folders (e.g. `/raw/`)  | `aws_s3_object`                        | [aws\_s3\_object](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_object)                                 |
| Enable versioning               | `versioning` block                     | [Bucket Versioning](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket#versioning)                    |
| Server-side encryption (AES256) | `server_side_encryption_configuration` | [SSE AES256](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket#server-side-encryption-configuration) |
| Tagging resources               | `tags` block                           | [S3 Tagging](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket#tags)                                 |

--- 

## 🧠 Glue Catalog

| Requirement             | Terraform Resource          | Documentation Link                                                                                                                          |
| ----------------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Create Glue Database    | `aws_glue_catalog_database` | [Glue Catalog Database](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/glue_catalog_database)                  |
| Define Glue Tables      | `aws_glue_catalog_table`    | [Glue Catalog Table](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/glue_catalog_table)                        |
| Define schema & formats | `storage_descriptor` block  | [Table Schema & Storage](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/glue_catalog_table#storage_descriptor) |

--- 

## ⚙️ Glue Job

| Requirement                        | Terraform Resource                   | Documentation Link                                                                                                           |
| ---------------------------------- | ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Create Glue Job                    | `aws_glue_job`                       | [Glue Job](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/glue_job)                             |
| Use Python 3.9 & Glue version 3.0  | `python_version`                     | [Job Configuration](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/glue_job#command)            |
| Reference external script          | `script_location`                    | [Glue Script Location](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/glue_job#script_location) |
| Partition data by column in output | Script: `DynamicFrame.partitionBy()` | [Partitioning Data (AWS Docs)](https://docs.aws.amazon.com/glue/latest/dg/partitioning-data.html)                            |

--- 

## 🔍 Athena

| Requirement               | Terraform Resource           | Documentation Link                                                                                                                        |
| ------------------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Create Workgroup          | `aws_athena_workgroup`       | [Athena Workgroup](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/athena_workgroup)                          |
| Set query result location | `result_configuration` block | [Result Configuration](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/athena_workgroup#result_configuration) |
| Define named query        | `aws_athena_named_query`     | [Athena Named Query](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/athena_named_query)                      |

--- 

## 🔐 IAM Roles and Policies

| Requirement                | Terraform Resource               | Documentation Link                                                                                                            |
| -------------------------- | -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Create IAM Role            | `aws_iam_role`                   | [IAM Role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role)                              |
| Add trust policy for Glue  | `assume_role_policy` block       | [Trust Relationship](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role#assume_role_policy) |
| S3/Glue permissions        | `aws_iam_role_policy`            | [IAM Policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy)                     |
| Attach managed Glue policy | `aws_iam_role_policy_attachment` | [Policy Attachment](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment)   |

--- 
