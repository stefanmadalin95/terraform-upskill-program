# 🏗️ Module 07: Intro to Data Lake Components (Terraform + AWS)

In this module, you’ll bring your Terraform skills into the **data world**.  
We’ll break down each component of a modern **data lake architecture** and show how it translates into AWS services and Terraform resources.

---

## 🧭 Learning Objectives

✅ Understand the **purpose** of each layer in a data lake  
✅ Learn how AWS services support data lake design  
✅ Explore which **Terraform modules** to use for each component  
✅ Prepare your final project infrastructure blueprint  
✅ Practice wiring together real infrastructure pieces before the final build

---

## 🧊 What Is a Data Lake?

A **data lake** is a centralized repository that allows you to store structured and unstructured data at any scale.

It typically includes:

| Layer             | Purpose                                   | AWS Example           |
|-------------------|-------------------------------------------|-----------------------|
| Storage Layer     | Store raw and curated datasets            | AWS S3                |
| Metadata Layer    | Describe and manage data structure        | AWS Glue Data Catalog |
| Access Layer      | Enable data exploration and reporting     | IAM Roles, Athena     |
| Processing Layer  | Execute and manage data processing jobs   | AWS Glue Jobs         |

---

## 🧰 Services You’ll Work With

| Terraform Module      | AWS Service           | Purpose                              |
|-----------------------|-----------------------|--------------------------------------|
| `aws_s3_bucket`       | Amazon S3             | Store raw, curated, processed data   |
| `aws_glue_catalog_*`  | AWS Glue Data Catalog | Allow jobs/users to interact with data |
| `aws_athena_database` | Amazon Athena         | Organize metadata for datasets       |
| `aws_iam_role/policy` | IAM                   | Query the data lake                  |
| `aws_glue_job`        | AWS Glue              | Trace cost and ownership             |

---

## 🧪 Hands-on Exercises

👉 See the [exercises folder](./exercises)

✅ [Exercise 1: Create Unique S3 Bucket and Directory](exercises/exercise-1.md)  
✅ [Exercise 2: Create Glue Catalog Database and Table](exercises/exercise-2.md)  
✅ [Exercise 3: Connect Athena to Glue Catalog](exercises/exercise-3.md)  
✅ [Exercise 4: Create IAM Role for Catalog Access](exercises/exercise-4.md)  
✅ [Exercise 5: Create Glue Job to Query Catalog Data](exercises/exercise-5.md)


---

## 🔗 References

Explore deeper AWS Data Lake best practices in [references](references.md).

---

## 🎉 Ready for the Final Integration?

✅ Once you’ve practiced with these components, proceed to [Module 08: Final Project](../module-08-final_project/README.md).

Happy building and exploring! 🚀✨
