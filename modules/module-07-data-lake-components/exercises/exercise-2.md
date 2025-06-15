# 🧩 Exercise 2: Create Glue Catalog Database and Table

## 🎯 Objective

Create a Glue Data Catalog **database** and define a basic **table schema** that points to your raw data stored in S3. This exercise introduces you to the metadata layer of the data lake.

---

## 🧱 What You’ll Build

- A **Glue Catalog Database** named `data_lake_metadata`
- A **Glue Catalog Table** named `raw_layer`
- Table metadata that defines structure and format (CSV-based)
- S3 location linked to the `raw/` prefix created in Exercise 1

---

## 🪜 Steps

### ✅ Step 1: Create a New Module

Create a new module called `glue_catalog_metadata/`.

#### `main.tf`

```hcl
resource "aws_glue_catalog_database" "this" {
  name = var.database_name
}

resource "aws_glue_catalog_table" "this" {
  name          = var.table_name
  database_name = aws_glue_catalog_database.this.name
  table_type    = "EXTERNAL_TABLE"

  storage_descriptor {
    location      = var.s3_location
    input_format  = "org.apache.hadoop.mapred.TextInputFormat"
    output_format = "org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat"
    compressed    = false

    serde_info {
      serialization_library = "org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe"
      parameters = {
        "field.delim" = ","
      }
    }

    columns {
      name = "id"
      type = "string"
    }

    columns {
      name = "timestamp"
      type = "string"
    }
  }
}
```

### ✅ Step 2: Define Variables and Outputs

#### `variables.tf`

```hcl
variable "database_name" {
  description = "Glue catalog database name"
  type        = string
}

variable "table_name" {
  description = "Name of the table in the catalog"
  type        = string
}

variable "s3_location" {
  description = "S3 location to link this table to"
  type        = string
}
```

#### `outputs.tf`

```hcl
output "glue_database_name" {
  value = aws_glue_catalog_database.this.name
}

output "glue_table_name" {
  value = aws_glue_catalog_table.this.name
}
```

### ✅ Step 3: Call the Module

In your root configuration:

```hcl
module "glue_catalog_metadata" {
  source        = "./modules/glue_catalog_metadata"
  database_name = "data_lake_metadata"
  table_name    = "raw_layer"
  s3_location   = "s3://${module.data_lake_bucket.bucket_name}/raw/"
}
```

## 🔁 Run the Workflow

```bash
terraform init
terraform plan
terraform apply
```

## 🧠 Reflection
- What kind of schema do you typically define in Glue tables?
- Why is separating raw and curated metadata into different databases or tables beneficial?
- How could you adjust this table to support other formats like Parquet or JSON?